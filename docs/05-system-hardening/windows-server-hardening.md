# Durcissement du serveur Windows (Hardening)

[Accueil du laboratoire](../README.md) · [Accueil du dépôt](../../README.md)

## 1. Objectif

Réduire la surface d'attaque du contrôleur de domaine `SRV-DC01` en appliquant les bonnes pratiques de sécurité de base.

## 2. Contexte technique

Le contrôleur de domaine `SRV-DC01` héberge des services centraux d’identité et de résolution ; sa compromission peut avoir un impact important sur le domaine. Les mesures de protection doivent être validées sur ce rôle avant d’être considérées comme appliquées.

## 3. Mesures mentionnées et niveau de preuve

Les notes initiales déclarent l’activation du pare-feu, la désactivation de RDP, le renommage du compte Administrateur et la désactivation de SMBv1. Les captures annoncées pour le pare-feu et SMBv1 ne sont pas présentes dans le dépôt ; ces opérations ne sont donc pas confirmées ici.

Le renommage d’un compte Administrateur local n’est pas une mesure applicable telle quelle à un contrôleur de domaine : les contrôleurs n’utilisent pas la base locale des comptes comme un serveur membre standard. Les comptes privilégiés du domaine et le compte DSRM doivent être traités selon leur contexte propre.

## 4. Vérification de SMBv1

La capture système identifie Windows Server 2025. Selon Microsoft, SMBv1 n’est pas installé par défaut sur Windows Server 2019 et versions ultérieures ; ne pas présenter la désactivation comme effectuée sans vérifier l’état réel du composant.

Depuis une console PowerShell élevée, vérifier la configuration du serveur SMB :

```powershell
Get-SmbServerConfiguration | Select-Object EnableSMB1Protocol
```

La fonctionnalité Windows peut aussi être interrogée :

```powershell
Get-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
```

Si SMBv1 est effectivement activé, sa désactivation doit être planifiée et validée selon la procédure Microsoft correspondant à la version et au rôle du serveur. La désactivation peut nécessiter un redémarrage ou affecter des équipements anciens ; vérifier les dépendances avant changement.

## 5. Vérifications

Les commandes de lecture ci-dessus permettent de documenter l’état SMBv1. Pour le pare-feu, une sortie datée de `Get-NetFirewallProfile` reste à ajouter. Aucune sortie de vérification n’est actuellement archivée.

## 6. Captures d'écran

Les captures d’écran du pare-feu et de l’état SMBv1 mentionnées dans la version initiale ne sont pas présentes dans `screenshots/05-system-hardening/`. Elles restent à réaliser après vérification sur le serveur.

## 7. Résultat obtenu

**À vérifier.** Les mesures de durcissement sont décrites comme des objectifs ou des déclarations antérieures, sans preuve suffisante dans le dépôt pour confirmer leur état actuel.

## 8. Difficultés rencontrées

La désactivation de SMBv1 peut casser d'anciens équipements réseau (imprimantes, NAS). Il faut vérifier la compatibilité avant de le faire en production.

## 9. Conclusion

Le durcissement doit être mesuré et documenté à partir de la configuration réelle du serveur. La désactivation de protocoles ou de services doit être précédée d’une analyse d’impact et suivie de tests des services AD et DNS.

[GPO et stratégies de compte](gpo-implementation.md) · [Retour à l’index](../README.md)

## Références techniques

- Microsoft Learn — [Detect, enable, and disable SMBv1, SMBv2, and SMBv3 in Windows](https://learn.microsoft.com/en-us/windows-server/storage/file-server/troubleshoot/detect-enable-and-disable-smbv1-v2-v3)