
# Sécurisation de l'infrastructure DNS avec DNSSEC

[Accueil du laboratoire](../README.md) · [Accueil du dépôt](../../README.md)

> **Projet :** Infrastructure Active Directory — TechCorp  
> **Serveur DNS :** SRV-DC01  
> **Zone DNS :** `lab.local`  
> **Technologie :** Microsoft DNS Server / DNSSEC  
> **Catégorie :** Sécurité des infrastructures — Durcissement DNS

---

## 1. Objectif

L'objectif de cette opération est de renforcer la sécurité du service DNS hébergé sur le contrôleur de domaine `SRV-DC01`, en mettant en œuvre DNSSEC (*Domain Name System Security Extensions*).

DNSSEC est un ensemble d'extensions de sécurité du protocole DNS permettant de garantir :

- **L'authenticité des données DNS :** vérifier que les informations reçues correspondent aux données publiées par la zone légitime.
- **L'intégrité des réponses :** détecter toute modification non autorisée des données DNS pendant leur transmission.
- **La protection contre certaines attaques DNS :** réduire les risques d'empoisonnement de cache (*DNS Cache Poisoning*) et de falsification des réponses.

Cette opération s'inscrit dans une démarche globale de durcissement de l'infrastructure Active Directory de TechCorp.

## 2. Contexte technique

Le serveur `SRV-DC01` héberge le service DNS utilisé par les machines du laboratoire pour résoudre les noms des ressources du domaine `lab.local`.

Dans une infrastructure Active Directory, DNS joue un rôle essentiel. Il permet notamment :

- La localisation des contrôleurs de domaine.
- La découverte des services Active Directory.
- La résolution des noms des serveurs et des postes clients.
- Le fonctionnement des mécanismes d'authentification et de communication entre les machines.

### 2.1. Risques liés à un DNS non sécurisé

Un service DNS qui ne vérifie pas cryptographiquement l'authenticité des données peut être exposé à plusieurs risques :

| Menace | Description |
|---|---|
| DNS Spoofing | Injection de réponses DNS falsifiées. |
| DNS Cache Poisoning | Introduction de fausses associations nom/IP dans un cache DNS. |
| Altération des réponses | Modification des informations DNS pendant leur transmission. |
| Redirection frauduleuse | Orientation d'un utilisateur vers une adresse IP non légitime. |

DNSSEC apporte une protection cryptographique contre la falsification des données DNS, sous réserve que la chaîne de validation soit correctement configurée.

## 3. Principe de fonctionnement de DNSSEC

DNSSEC repose sur la cryptographie asymétrique et sur un système de signatures numériques.

Contrairement au DNS classique, qui fournit des réponses sans mécanisme cryptographique intégré permettant de vérifier leur authenticité, DNSSEC ajoute des signatures vérifiables aux données publiées dans une zone.

### 3.1. Les clés cryptographiques

La signature DNSSEC utilise principalement deux catégories de clés :

**KSK — Key Signing Key**

- Clé destinée à signer l'ensemble des enregistrements DNSKEY de la zone.
- Permet de protéger cryptographiquement les clés publiques publiées.
- Joue un rôle important dans l'établissement de la chaîne de confiance.

**ZSK — Zone Signing Key**

- Clé utilisée pour signer les ensembles d'enregistrements DNS de la zone.
- Permet de vérifier l'authenticité des informations DNS publiées.
- Est utilisée pour produire les signatures RRSIG correspondantes.

### 3.2. Les principaux enregistrements DNSSEC

| Enregistrement | Fonction |
|---|---|
| DNSKEY | Publie les clés publiques utilisées par DNSSEC. |
| RRSIG | Contient les signatures cryptographiques des ensembles d'enregistrements DNS. |
| DS | Permet de relier cryptographiquement une zone enfant à sa zone parente. |
| NSEC | Permet de prouver l'inexistence d'un nom DNS. |
| NSEC3 | Fournit un mécanisme alternatif de preuve de non-existence utilisant des empreintes cryptographiques. |

### 3.3. Fonctionnement général

Le mécanisme de validation suit généralement ce processus :

1. Le serveur DNS publie les enregistrements de sa zone.
2. Les ensembles d'enregistrements sont signés à l'aide de clés privées.
3. Les signatures correspondantes sont publiées sous forme d'enregistrements RRSIG.
4. Les clés publiques nécessaires à la vérification sont accessibles dans les enregistrements DNSKEY.
5. Le résolveur validant vérifie les signatures et la chaîne de confiance.
6. Si les vérifications réussissent, les données peuvent être considérées comme authentiques et intègres.

**Important :** DNSSEC ne chiffre pas les requêtes DNS. Il garantit l'authenticité et l'intégrité des données DNS, mais pas leur confidentialité.

## 4. Environnement technique

| Élément | Configuration |
|---|---|
| Serveur | SRV-DC01 |
| Système | Windows Server |
| Rôle | Contrôleur de domaine Active Directory |
| Service | DNS Server |
| Zone DNS | `lab.local` |
| Technologie de sécurisation | DNSSEC |
| Interface d'administration | PowerShell |
| Environnement | Laboratoire virtualisé |

## 5. Mise en œuvre de DNSSEC

### 5.1. Accès au serveur

La configuration a été réalisée directement sur le serveur `SRV-DC01`.

Les opérations nécessitent des privilèges administratifs.

1. Se connecter au serveur `SRV-DC01`.
2. Ouvrir le menu Démarrer.
3. Rechercher Windows PowerShell.
4. Effectuer un clic droit.
5. Sélectionner **Exécuter en tant qu'administrateur**.

### 5.2. Vérification de la zone DNS

Avant toute modification, vérifier que la zone `lab.local` existe :

```powershell
Get-DnsServerZone -Name "lab.local"
```

Cette commande permet de consulter les propriétés de la zone DNS hébergée par le serveur.

### 5.3. Signature de la zone DNS

La commande suivante permet de lancer la signature DNSSEC de la zone à l'aide des paramètres par défaut du serveur Microsoft DNS :

```powershell
Invoke-DnsServerZoneSign -ZoneName "lab.local" -SignWithDefault -Force
```

**Explication des paramètres :**

- `Invoke-DnsServerZoneSign` : lance le processus de signature DNSSEC.
- `-ZoneName "lab.local"` : désigne la zone à signer.
- `-SignWithDefault` : utilise les paramètres de signature par défaut.
- `-Force` : autorise l'exécution sans demander certaines confirmations interactives.

La documentation Microsoft précise que cette option signe une zone non signée avec une KSK et une ZSK suivant les paramètres par défaut. Vérifier l’état avant toute exécution : une re-signature d’une zone déjà signée est une opération distincte (`-DoResign`) et ne doit pas être déclenchée sans plan de changement et sauvegarde.

### 5.4. Vérification de l'état de signature

Après l'opération, exécuter :

```powershell
Get-DnsServerZone -Name "lab.local" |
Select-Object ZoneName, IsSigned
```

Résultat attendu :

```text
ZoneName    IsSigned
--------    --------
lab.local   True
```

La valeur `True` indique que la zone est identifiée comme signée par le serveur DNS.

### 5.5. Vérification des enregistrements DNSSEC

Pour vérifier la présence des enregistrements DNSKEY :

```powershell
Get-DnsServerResourceRecord -ZoneName "lab.local" -RRType DNSKEY
```

Pour consulter les enregistrements RRSIG :

```powershell
Get-DnsServerResourceRecord -ZoneName "lab.local" -RRType RRSIG
```

Ces vérifications permettent de constater la présence des données associées à la signature DNSSEC.

### 5.6. Vérification des propriétés DNSSEC

Pour examiner les propriétés de signature de la zone :

```powershell
Get-DnsServerDnsSecZoneSetting -ZoneName "lab.local"
```

Cette commande permet de consulter les paramètres DNSSEC associés à la zone.

## 6. Configuration de la validation DNSSEC

La signature d'une zone et la validation DNSSEC sont deux mécanismes distincts.

- **Signature :** le serveur signe cryptographiquement les données de sa propre zone.
- **Validation :** le résolveur DNS vérifie les signatures reçues et la chaîne de confiance associée.

Sur `SRV-DC01`, la validation DNSSEC des réponses externes a également été activée dans les propriétés du serveur DNS.

Cette configuration concerne le rôle de résolveur du serveur et ne signifie pas automatiquement que tous les clients du réseau effectuent eux-mêmes une validation cryptographique.

Il faut également distinguer la validation des réponses DNS externes de la signature de la zone interne `lab.local`.

La capture des enregistrements de zone montre les adresses `192.168.56.10` et `10.0.3.15` pour `SRV-DC01`. Dans un serveur doté de plusieurs interfaces, vérifier quels enregistrements sont publiés et quelle adresse est renvoyée aux clients avant de conclure que la résolution est correcte.

## 7. Vérifications et contrôles

Les contrôles suivants permettent d'évaluer le fonctionnement de la configuration.

| Contrôle | Résultat attendu |
|---|---|
| Existence de la zone | `lab.local` présente |
| État de signature | `IsSigned : True` |
| Présence des DNSKEY | Enregistrements disponibles |
| Présence des RRSIG | Signatures disponibles |
| Résolution DNS classique | Fonctionnelle |
| Connectivité du laboratoire | Maintenue |

### 7.1. Vérification de la résolution DNS

Depuis un poste client du laboratoire :

```powershell
nslookup lab.local
```

Cette commande permet de vérifier que la résolution DNS reste opérationnelle.

**Attention :** une résolution réussie avec `nslookup` ne prouve pas à elle seule que la validation DNSSEC est effective.

Pour démontrer une validation complète, il faut vérifier le statut de validation auprès d'un résolveur validant et contrôler la chaîne de confiance.

## 8. Captures d'écran et preuves techniques

Les captures suivantes documentent les principales étapes de configuration.

### Figure 1 — Activation de la validation DNSSEC

Présentation de la configuration de validation DNSSEC dans les propriétés du serveur DNS.

![Activation de la validation DNSSEC](../../screenshots/06-dns-security/dnssec-validation-settings.png)

### Figure 2 — Paramètres DNSSEC de la zone `lab.local`

La capture montre les paramètres du maître de clés et leur état, pas l’exécution de la commande PowerShell.

![Paramètres de clés DNSSEC de la zone lab.local](../../screenshots/06-dns-security/dnssec-key-settings.png)

### Figure 3 — Enregistrements DNSSEC visibles dans la zone

La capture DNS affiche notamment des enregistrements `RRSIG` et `NSEC3`. Elle documente la présence d’enregistrements de signature, mais ne montre pas la sortie de `Get-DnsServerZone` ni un résultat de validation côté client.

![Enregistrements RRSIG et NSEC3 de la zone](../../screenshots/06-dns-security/dnssec-signed-records.png)

### Figure 4 — Vérification des enregistrements DNSSEC

La validation de la présence des enregistrements DNSKEY et RRSIG est un contrôle complémentaire essentiel pour confirmer que la signature DNSSEC a bien été appliquée à la zone `lab.local`.

Les commandes suivantes doivent permettre d'afficher les clés publiques publiées et les signatures générées par le serveur :

```powershell
Get-DnsServerResourceRecord -ZoneName "lab.local" -RRType DNSKEY
Get-DnsServerResourceRecord -ZoneName "lab.local" -RRType RRSIG
```

Le résultat attendu est la présence des enregistrements DNSSEC applicables. La capture conservée montre `RRSIG` et `NSEC3`, mais aucune sortie PowerShell de ces commandes ni capture des `DNSKEY` n’est archivée.

### Figure 5 — Vérification de la résolution DNS

Le test de résolution DNS depuis un poste client vise à confirmer que la zone signée reste accessible et que les services du laboratoire continuent de fonctionner correctement après l'activation de DNSSEC.

```powershell
nslookup lab.local
```

Cette commande permet de contrôler la résolution classique du nom, mais pas de prouver à elle seule la validation DNSSEC. Aucune capture du test client n’est présente dans le dépôt. Le statut de validation doit être contrôlé auprès d’un résolveur validant et avec une chaîne de confiance appropriée.

## 9. Difficultés et points d'attention

La mise en œuvre de DNSSEC sur une infrastructure Active Directory nécessite de prendre en compte plusieurs éléments.

**9.1. Compatibilité des résolveurs**

Les clients et les résolveurs doivent disposer des capacités nécessaires pour prendre en charge le mécanisme de validation attendu.

**9.2. Gestion des clés**

Les clés cryptographiques doivent être correctement protégées et renouvelées selon une politique adaptée.

**9.3. Chaîne de confiance**

La signature d'une zone ne suffit pas à établir automatiquement une chaîne de confiance complète.

Dans le cas de `lab.local`, le suffixe `.local` est désigné pour l’usage spécial de mDNS (RFC 6762) et ne possède pas de délégation publique DNSSEC classique remontant à la racine.

Une architecture de confiance interne doit donc être étudiée si l'objectif est de valider cryptographiquement cette zone depuis des résolveurs indépendants.

**9.4. Continuité du service**

Toute modification DNSSEC doit être suivie de tests de résolution afin de s'assurer que les services Active Directory restent accessibles.

## 10. Résultat obtenu

Les preuves visuelles montrent le paramètre de validation DNSSEC des réponses distantes activé sur le serveur et des enregistrements `RRSIG`/`NSEC3` dans `lab.local`. Le texte du laboratoire rapporte également `IsSigned : True`, mais la sortie de cette commande n’est pas archivée. La validation DNSSEC par les clients, la chaîne de confiance interne et la continuité de la résolution AD restent à vérifier ; la capture `dcdiag` disponible signale par ailleurs un échec DNS/DC locator.

## 11. Conclusion

La mise en œuvre de DNSSEC constitue une étape importante dans le durcissement du service DNS d'une infrastructure Active Directory.

Grâce à la signature cryptographique des données DNS, il devient possible de détecter les modifications non autorisées et de vérifier l'authenticité des informations publiées.

Ce travail permet également de mieux comprendre le fonctionnement des clés cryptographiques, des signatures numériques et des mécanismes de validation DNS.

DNSSEC vient ainsi compléter les autres mesures de sécurisation de l'infrastructure, notamment le durcissement d'Active Directory, la sécurisation des comptes et la surveillance des services réseau.

---

## 12. Références techniques

- Microsoft Learn — DNSSEC Overview: https://learn.microsoft.com/en-us/windows-server/networking/dns/dnssec-overview
- Microsoft Learn — DNS Server PowerShell: https://learn.microsoft.com/en-us/powershell/module/dnsserver/
- Microsoft Learn — [Invoke-DnsServerZoneSign](https://learn.microsoft.com/en-us/powershell/module/dnsserver/invoke-dnsserverzonesign?view=windowsserver2025-ps)
- Microsoft Learn — [Get-DnsServerResourceRecord](https://learn.microsoft.com/en-us/powershell/module/dnsserver/get-dnsserverresourcerecord?view=windowsserver2025-ps)
- Microsoft Learn — [Get-DnsServerDnsSecZoneSetting](https://learn.microsoft.com/en-us/powershell/module/dnsserver/get-dnsserverdnsseczonesetting?view=windowsserver2025-ps)
- RFC 4033 — DNS Security Introduction and Requirements: https://www.rfc-editor.org/rfc/rfc4033
- RFC 4034 — Resource Records for DNS Security Extensions: https://www.rfc-editor.org/rfc/rfc4034
- RFC 4035 — Protocol Modifications for DNS Security Extensions: https://www.rfc-editor.org/rfc/rfc4035
- RFC 6762 — Multicast DNS (usage spécial du suffixe `.local`) : https://www.rfc-editor.org/rfc/rfc6762

[Résultats d’audit](../07-security-audit/audit-results.md) · [Plan de remédiation](../08-remediation/remediation-plan.md) · [Retour à l’index](../README.md)
