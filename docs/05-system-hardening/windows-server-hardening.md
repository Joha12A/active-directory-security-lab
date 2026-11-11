# Durcissement du serveur Windows (Hardening)

## 1. Objectif

Réduire la surface d'attaque du contrôleur de domaine `SRV-DC01` en appliquant les bonnes pratiques de sécurité de base.

## 2. Contexte technique

Le serveur `SRV-DC01` est le composant le plus critique de l'infrastructure. S'il est compromis, c'est tout le domaine qui tombe. Il doit donc être protégé en priorité.

## 3. Configuration réalisée

*   **Pare-feu Windows** : Activé sur tous les profils (Domaine, Privé, Public).
*   **Bureau à distance (RDP)** : Désactivé par défaut (sauf si nécessaire pour l'administration).
*   **Comptes administrateurs locaux** : Le compte "Administrateur" local a été renommé pour compliquer les attaques par force brute.
*   **Mises à jour** : Windows Update est configuré pour installer les mises à jour automatiquement.
*   **Désactivation de SMBv1** : Le protocole obsolète et vulnérable SMBv1 a été désactivé.

## 4. Procédure (Exemple avec SMBv1)

1. Ouverture de PowerShell en mode Administrateur.
2. Exécution de la commande : `Disable-WindowsOptionalFeature -Online -FeatureName smb1protocol`
3. Redémarrage du serveur.

## 5. Vérifications

Vérification de l'état du pare-feu avec `Get-NetFirewallProfile` et vérification de l'absence de SMBv1.

## 6. Captures d'écran

**Figure 1 — État du pare-feu Windows**
![Pare-feu Windows](../../screenshots/05-system-hardening/windows-firewall-status.png)

**Figure 2 — Désactivation de SMBv1 via PowerShell**
![Désactivation SMBv1](../../screenshots/05-system-hardening/smbv1-disabled.png)

## 7. Résultat obtenu

Le serveur est mieux protégé contre les attaques réseau de base et les protocoles obsolètes.

## 8. Difficultés rencontrées

La désactivation de SMBv1 peut casser d'anciens équipements réseau (imprimantes, NAS). Il faut vérifier la compatibilité avant de le faire en production.

## 9. Conclusion

Le durcissement d'un serveur est un processus continu. Ces premières mesures constituent une base saine pour le contrôleur de domaine.