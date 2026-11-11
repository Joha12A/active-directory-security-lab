# Méthodologie d'audit de sécurité

## 1. Objectif

Définir l'approche méthodologique pour l'audit de sécurité de l'infrastructure TechCorp depuis une machine d'attaque (Kali Linux).

## 2. Périmètre de l'audit

L'audit se concentrera sur les éléments suivants :
*   **Contrôleur de domaine** (`SRV-DC01`) : Surface d'attaque réseau, services exposés.
*   **Service DNS** : Résistance aux attaques par empoisonnement de cache (test de la validation DNSSEC).
*   **Protocoles d'authentification** : Résistance aux attaques par force brute sur Kerberos et NTLM.

## 3. Outils prévus

*   **Nmap** : Cartographie du réseau et découverte des services.
*   **Enum4linux / LDAPSearch** : Énumération de l'annuaire Active Directory.
*   **Hydra** : Tests de robustesse des mots de passe (si autorisé dans le lab).
*   **Responder** : Détection des faiblesses liées aux protocoles LLMNR/NBT-NS.

## 4. Statut

**⚠️ En cours de développement.**

La mise en place de l'environnement d'attaque (connectivité entre la machine Kali et le réseau interne `labnet`) a rencontré des contraintes techniques liées à la virtualisation (isolation du réseau Host-Only). La documentation de cette phase sera complétée dès que l'infrastructure réseau d'audit sera pleinement opérationnelle.