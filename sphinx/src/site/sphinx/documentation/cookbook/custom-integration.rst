Où placer vos intégration personnalisées
========================================

Dans le dossier de configuration d'ARender (HMI ou rendition) se situent deux fichiers permettant d'ajouter des intégrations personnalisées pour ARender.

Ces fichiers sont vides par défaut et permettent à chaque version de recopier l'intégrtation personnalisée facilement sans se soucier du contenu de ce fichier.

Le but est d'éviter les conflits d'écrasement de version, mais il reste important de vérifier les nouveaux paramètres pour garder sa version d'ARender à jour.

Dans la rendition:
        - conf/arender-rendition-custom-integration.xml
Dans l'HMI:
        - WEB-INF/classes/arender-custom-integration.xml (configuration de la GUI utilisateur)
        - WEB-INF/classes/arender-custom-server-integration.xml (configuration du serveur)

