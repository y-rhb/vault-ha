# Exploiter un cluster Vault en haute disponibilité

Vault servait de point central pour les secrets du projet SLLYM. Cette sélection montre comment le service suivait le changement de nœud actif et comment ses journaux d’audit étaient gérés.

## Dans ce dépôt

- [Keepalived](ansible/roles/keepalived/tasks/main.yml) déploie les sondes et la configuration de l’adresse IP virtuelle partagée. La [sonde du nœud actif](ansible/roles/keepalived/templates/check_vault_leader.sh.j2) distingue le rôle du nœud de son état de santé.
- [Rotation des journaux d’audit](ansible/roles/audit_logrotate/tasks/main.yml) met en place la politique de rotation du fichier de journal.
- [Extension du stockage](ansible/roles/disk_expansion/tasks/main.yml) automatise l’ajustement des volumes logiques.

## Projet d’origine et réutilisation

Le projet de fin d’études SLLYM, réalisé en équipe à l’ESGI, déployait un cluster Vault sur vSphere avec réplication Raft, déverrouillage via AWS KMS, émission de certificats et authentification des pipelines par jetons signés. Ce dépôt présente trois rôles d’exploitation. Ils s’utilisent avec un cluster Vault existant, un inventaire et des variables propres à l’environnement.
