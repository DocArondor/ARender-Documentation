------------------------------------
Installation du serveur de rendition
------------------------------------

Méthode à suivre pour installer le serveur de rendition

Installation
============

*Les zones en gras doivent être modifiées suivant vos versions/situations*

Lancer l'assistant d'installation du serveur de rendition. Pour cela différents biais peuvent être utilisés :

- Double cliquer sur le fichier arondor-arender-rendition-service-{NUMÉRO-VERSION}.jar (**en mode administrateur**)

- Ou en ligne de commande **en mode administrateur** ::

    java –jar arondor-arender-rendition-service{NUMÉRO-VERSION}.jar

Pour une installation en mode hors interface graphique, exécuter la commande suivante ::

    java –jar arondor-arender-rendition-service{NUMÉRO-VERSION}.jar -console

Pour une installation en mode silencieux, exécuter la commande suivante (lien vers le fichier de propriétés :download:`installer.properties </_static/docs/installer.properties>`) ::

    java –jar arondor-arender-rendition-service{NUMÉRO-VERSION}.jar -options installer.properties

- L'écran d'accueil suivant s’affiche et cliquer sur "Next" :

.. image:: /_static/images/Welcome_highlighted.png
    :align: center

- Choisir le répertoire d'installation et cliquer sur "Next" :

.. image:: /_static/images/img2_highlighted.png
    :align: center

- Dans la fenêtre des choix de composants à installer, cliquer sur "Next" pour installer les composants par défaut:

.. image:: /_static/images/img3_highlighted.png
    :align: center


- Une fois l'installation du serveur de rendition terminée, cliquer sur "Next" :

.. image:: /_static/images/img4_highlighted.png
    :align: center

- Entrer les paramètres de configuration correspondant à l'environnement.
    * Pour lancer ARender en tant que service, cocher "Run ARender as service". Cela permet de lancer ARender pour le tester lors des étapes suivantes.
    * Dans le cas ou vous ne voulez pas ARender en tant que service, laisser décocher "Run ARender as service".

        :ref:`Lancement manuel du service ARender Rendition <LancementManuel>`.

- Puis cliquer sur "Next"

.. image:: /_static/images/img31_highlighted.png
    :align: center


Une fois la configuration terminée , cliquer sur "Next". Si une erreur apparaît, reportez vous à la :ref:`FAQ<FAQ>`. (*un problème d'encodage de la police peut survenir lors des cet étape mais ne nuit pas à l'installation*)

.. image:: /_static/images/img6_highlighted.png
    :align: center

- Cliquer sur "Done" pour terminer l'installation

.. image:: /_static/images/img7_highlighted.png
    :align: center

