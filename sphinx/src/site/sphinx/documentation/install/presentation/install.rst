--------------------------------------
Déploiement du serveur de présentation
--------------------------------------

Déploiement avec Jetty
======================

* Récupérer "jetty-runner-**{NUMÉRO-VERSION}**.jar"
* Récupérer "arondor-arender-hmi-**{NUMÉRO-VERSION}**.war"
* Placer ces fichiers dans un dossier (exemple : "C:\ARender")

Une fois les fichiers récupérés et stockés :

* Ouvrir une invite de commande et taper ::

    cd C:\ARender

Par défaut, le fichier à modifier est arender.xml : si le serveur de rendition est installé sur un autre serveur que celui de présentation ou s’il utilise un autre port que celui par défaut (**1789**), et/ou si le Content Engine est sur un autre serveur que celui de présentation ou s’il utilise un autre port que celui par défaut (**2809**).

Pour lancer le serveur jetty avec le war présent dans le dossier courant, taper la commande suivante dans l'invite de commande ::

    java -jar jetty-runner-{NUMÉRO-VERSION}.jar arondor-arender-hmi-{NUMÉRO-VERSION}.war

.. image:: /_static/images/img15_highlighted.png
    :align: center

Déploiement dans WebSphere
==========================

* Ouvrir une console WebSphere
(« https://serveur_websphere:9043/ibm/console »)

.. image:: /_static/images/img19_highlighted.png
    :align: center
    :width: 100%

* Aller dans l’onglet « Applications », puis cliquer sur « Applications d’entreprise »

.. image:: /_static/images/img20_highlighted.png
    :align: center
    :width: 100%

* Pour lancer l’installation, cliquer sur « Installer »

.. image:: /_static/images/img21_highlighted.png
    :align: center
    :width: 100%

* Choisir le chemin de l’EAR à déployer et cliquer sur « Suivant »

.. image:: /_static/images/img22_highlighted.png
    :align: center
    :width: 100%

* Pour accepter les paramètres par défaut, cliquer sur « Suivant »

.. image:: /_static/images/img23_highlighted.png
    :align: center
    :width: 100%

* Sélectionner le(s) webserver(s) et/ou serveur(s), puis cliquer sur « Suivant »

.. image:: /_static/images/img24_highlighted.png
    :align: center
    :width: 100%

* Pour accepter les paramètres par défaut (hôte virtuel : default_host), cliquer sur « Suivant »

.. image:: /_static/images/img25_highlighted.png
    :align: center
    :width: 100%

* Dans la fenêtre récapitulative de l’installation, cliquer sur « Terminer » pour procéder à l’installation avec ces paramètres après les avoir vérifiés

.. image:: /_static/images/img26_highlighted.png
    :align: center
    :width: 100%

* Cliquer sur « Sauvegarder » afin de terminer l’installation

.. image:: /_static/images/img27_highlighted.png
    :align: center
    :width: 100%

* Pour démarrer « ARender HMI », cocher la case "ARenderHMI" puis cliquer sur « Démarrer »

.. image:: /_static/images/img28_highlighted.png
    :align: center
    :width: 100%


**Attention à l'ordre de chargement des libraires**

Il faut s'assurer que l'ordre de chargement des librairies soient configuré de telle sorte de Websphere charge ses librairies en dernier.

Procédure de vérification :

Tout d'abord :

* Dans la liste des applications cliquer sur ARenderHMI
* Cliquer sur « Chargement de classes et détection de mise à jour »
* Sélectionner « Classes chargées en premier avec un chargeur de classe local (dernier parent) »

.. image:: /_static/images/ChargementClasse_ParentLast_large.png
    :align: center
    :width: 100%

* Cliquer sur OK
Ensuite pour **un Websphere en version supérieur à 8** :

* Dans la liste des applications cliquer sur ARenderHMI
* Cliquer sur Gestion des modules
* Cliquer sur le module ARender
* Sélectionner, dans la liste déroulante « Ordre du chargeur de classes » : "Classes chargées en premier avec un chargeur de classe local (dernier parent)

.. image:: /_static/images/DernierParent_large.png
    :align: center
    :width: 100%

* Cliquer sur OK

Note:

Lorsque vous déployez ArenderHMI dans WebSphere Application Server, déployez ArenderHMI et IBM Content Navigator dans des profils (jvm) différents.

Afin de permettre l'utilisation de la session utilisateur (ICN) au sein d'ArenderHMI, vous devez mettre en place LTPA, comme suit :

Si LTPA a déjà été configuré sur d'autres profils, passer directement à l'import des clés. Sinon, exporter les clefs depuis l'un des profils WebSphere

Dans la console d'administration WebSphere, rendez-vous sur la page **Sécurité** > **Sécurité Globale**, dans la partie **Authentification**, cliquer sur **LTPA**


.. image:: /_static/images/Configuration-LTPA_highlighted.png
    :align: center
    :width: 100%

Renseigner un mot de passe, un chemin d'export, puis cliquer sur "Exporter les clés"

.. image:: /_static/images/Export-LTPA-key_highlighted.png
    :align: center
    :width: 100%

Une fois les clés exportées, importez-les dans le profil courant.

Sauvegarder les modifications

Redémarrer le profil WebSphere

Copier le fichier de clés sur le serveur où sera déployé ArenderHMI

Enfin, importer les clés dans le profil hébergeant ArenderHMI depuis la console d'administration WebSphere

1. Dans la console d'administration WebSphere, rendez-vous sur la page **Sécurité** > **Sécurité Globale**, dans la partie **Authentification**, cliquer sur **LTPA**

.. image:: /_static/images/Configuration-LTPA_highlighted.png
    :align: center
    :width: 100%

2. Renseigner le même mot de passe que précédemment
3. Renseigner le chemin du fichier contenant les clés
4. Cliquer sur "Importer les clés"
5. Sauvegarder les modifications
6. Redémarrer le profil


Utilisation de EARMaker
=======================

**Installation du serveur de présentation avec EARMaker**

**Méthode :**

* Récupérer l’EAR « arondor-arender-hmi-filenet-**{NUMÉRO-VERSION}**.ear »

* Récupérer l’utilitaire « earmaker-X-jar-with-dependencies.jar »

* Placer ces jar dans un dossier (exemple : « C:\\ARender »)

.. image:: /_static/images/img16.png
    :align: center

* Ouvrir une invite de commande et aller dans ce dossier « cd C:\\ARender »

* Par défaut, les fichiers à modifier sont :

* arender.xml : Si le serveur de rendition est installé sur un autre serveur que celui de présentation ou s’il utilise un autre port que celui par défaut (**1789**), et/ou si le Content Engine est sur un autre serveur que celui de présentation ou s’il utilise un autre port que celui par défaut (**2809**)

* Pour extraire et modifier ces fichiers, taper dans l’invite de commande ::

    java –jar earmaker-X-jar-with-dependencies.jar  –f (arender.xml,WcmApiConfig.properties) –s arondor-arender-hmi-filenet-{NUMÉRO-VERSION}.ear –t extraction

.. image:: /_static/images/img17.png
    :align: center


* Dans le dossier d’extraction (« C:\\ARender\\extraction »), modifier les fichiers à modifier spécifiés dans la commande.

* Pour incorporer les fichiers modifiés dans l’EAR final, dans la même invite de commandes taper ::

    « java –jar earmaker-X-jar-with-dependencies.jar  –m extraction –s arondor-arender-hmi-filenet-{NUMÉRO-VERSION}.ear –t arondor-arender-hmi-filenet-{NUMÉRO-VERSION}-earmaker.ear »

.. image:: /_static/images/img18.png
    :align: center

* L’EAR est recomposé et se trouve dans le dossier « C:\\ARender »

