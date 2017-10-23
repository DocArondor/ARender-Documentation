----------
Par défaut
----------

Ce connecteur est celui fourni par défaut et est utilisé par les mécanismes standards au produit. Il répond au paramètres de l'URL listés dans le tableau suivant :

    ===================================      ===============================================================================================
    Paramètre                                Description          
    ===================================      ===============================================================================================
    url                                      Permet de fournir une URL basée sur les protocoles HTTP et FTP
    uuid                                     Utilisé pour fournir l'identifiant d'un document généré au préalable par ARender (Avancé)
    bean                                     Utilisé pour spécifié un connecteur (Avancé)
    ===================================      ===============================================================================================

* Exemple ::

    Ouverture d'un document stocké sur le web
    http://arender.arondor.com/ARender/ARender.jsp?url=...

    Ouverture d'un document via un connecteur spécifique en propageant un identifiant et un jeton de sécurité
    http://{serveur_arender}/ARender.jsp?bean=monConnecteur&identifiant=123456&token=9GISU9SG4Z 

