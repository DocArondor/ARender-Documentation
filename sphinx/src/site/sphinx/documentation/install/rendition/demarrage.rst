----------------
Lancement manuel
----------------

**Si ARender n'a pas été installé en tant que service, il y a deux moyens de lancer le service ARender Rendition :**


Installation manuelle du service ARender Rendition sous Windows
===============================================================

Se rendre dans le dossier « bin » du répertoire d’installation d’ARender (par défaut : C:\\Program Files\\ARender-**{NUMÉRO-VERSION}**\\bin) :

.. image:: /_static/images/img11.png
	:align: center

* Double cliquer sur InstallService-ARenderServer.bat afin de mettre en service le serveur de rendition

* Vérifier que le service est bien installé et démarrer le service

.. image:: /_static/images/img12.png
	:align: center

.. _LancementManuel:

Lancement manuel sans installation du service ARender Rendition
===============================================================

Il est possible de lancer le service ARender manuellement via ligne de commande :

* Sous Windows avec ARenderServer.bat situé dans le répertoire ARender-Rendition-{NUMÉRO-VERSION}\\bin ::

	C:\Program Files\ARender-Rendition-{NUMÉRO-VERSION}\bin> ARenderServer.bat

* Sous Linux avec **ARenderServer-Console.sh** situé dans le répertoire ARender-Rendition-**{NUMÉRO-VERSION}**/bin ::

	~/ARender-Rendition{NUMÉRO-VERSION}/bin$ ./ARenderServer-Console.sh

