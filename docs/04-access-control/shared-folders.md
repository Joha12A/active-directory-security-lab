# Création et configuration des partages réseau

## 1. Objectif

Mettre à disposition un espace de stockage réseau sécurisé pour le service informatique (IT) de TechCorp, tout en garantissant la confidentialité des données vis-à-vis des autres services.

## 2. Contexte technique

Le serveur `SRV-DC01` héberge le contrôleur de domaine. Un dossier physique a été créé à la racine du disque `C:` pour accueillir les partages. Le groupe de sécurité `GRP_IT` a été utilisé pour définir les autorisations.

## 3. Configuration réalisée

*   **Chemin physique** : `C:\Partages\IT`
*   **Chemin réseau (UNC)** : `\\SRV-DC01\IT`
*   **Permissions de partage (SMB)** : Le groupe "Tout le monde" a été supprimé. Seul le groupe `GRP_IT` possède les droits de **Contrôle total**.
*   **Permissions NTFS (Sécurité)** : Seul le groupe `GRP_IT` possède les droits de **Modification** et **Écriture**.

## 4. Procédure

1. Création du dossier `IT` dans `C:\Partages\`.
2. Clic droit sur le dossier > **Propriétés** > Onglet **Partage**.
3. Clic sur **Partage avancé**, puis **Autorisations**.
4. Suppression du groupe "Tout le monde" (Everyone) par mesure de sécurité.
5. Ajout du groupe `GRP_IT` avec les droits de Contrôle total.
6. Onglet **Sécurité** (NTFS) : ajout du groupe `GRP_IT` avec les droits de Modification.

## 5. Vérifications

Les tests d'accès seront réalisés depuis le client `CLIENT-W10` avec différents comptes utilisateurs pour valider le cloisonnement.

## 6. Captures d'écran

**Figure 1 — Dossier partagé IT**
![Dossier partagé](../../screenshots/04-access-control/it-shared-folder.png)

**Figure 2 — Permissions de partage (SMB)**
![Permissions de partage](../../screenshots/04-access-control/it-share-permissions.png)

**Figure 3 — Permissions NTFS**
![Permissions NTFS](../../screenshots/04-access-control/it-ntfs-permissions.png)

## 7. Résultat obtenu

Le dossier est partagé sur le réseau et sécurisé. Seuls les membres du groupe `GRP_IT` sont censés pouvoir y accéder.

## 8. Difficultés rencontrées

Il est important de faire la différence entre les permissions de partage (qui s'appliquent lors de l'accès par le réseau) et les permissions NTFS (qui s'appliquent en local et sur le réseau). Les deux doivent être configurées correctement.

## 9. Conclusion

La mise en place d'un partage sécurisé est une tâche courante en administration système. L'utilisation des groupes de sécurité simplifie énormément la gestion au quotidien.