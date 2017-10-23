=======
Profils
=======

**Profils fournis**

ARender est livré avec les deux profils décrits ci-dessous.


    ===================================    =====================================================================================================
    Nom                                    Description          
    ===================================    =====================================================================================================
    Base : arender-default.properties      Fichier de configuration par défaut offrant une configuration de base pour une utilisation standalone    
    arender                                Profil par défaut pour une visualisation standard
    book                                   Profil permettant une visualisation de type livre
    jsapi-demo                             Profil démontrant les capacités de l'API Javascript ARender
    ===================================    =====================================================================================================

* Exemple ::

    Utilisation d'un profil spécifique
    http://arender.arondor.com/ARender/ARender.jsp?url=../samples/arender-en.pdf&props=book

**Ajout d'un profil**

Pour ajouter un profil, il est conseillé de partir du fichier par défaut (*arender.properties*) situé dans le répertoire *WEB-INF/classes* de l'application web à déployer pour créer un nouveau profil. Il suffira de modifier ce nouveau fichier en se référant à ce guide.
    
