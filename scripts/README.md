# Scripts et configurations

Ce répertoire ne contient actuellement aucun script PowerShell ou Bash suivi par Git. Les sous-répertoires locaux `bash/` et `powershell/` sont vides ; aucune automatisation n’est donc présentée comme disponible ou testée.

Les procédures exécutables documentées se trouvent dans les guides correspondants :

- [Installation AD DS](../docs/02-active-directory/adds-installation.md)
- [GPO et stratégies de compte](../docs/05-system-hardening/gpo-implementation.md)
- [Durcissement Windows Server](../docs/05-system-hardening/windows-server-hardening.md)
- [DNSSEC](../docs/06-dns-security/dnssec-implementation.md)

Avant d’ajouter un script, documenter son objectif, les privilèges requis, les effets de bord, les prérequis, les commandes de vérification et les limites. Aucun secret ne doit être stocké dans le code ou dans l’historique Git.