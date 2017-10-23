----------------------
Comparer des documents
----------------------


Comment mettre deux documents en comparaison ?
==================================================

Lancement manuel
----------------

Pour activer la comparaison de deux documents, effectuer un clic droit dans le volet de navigation au niveau du document à comparer avec celui en cours de visualisation.

.. image:: /_static/images/documentCompare1.png
    :align: center
    :width: 100%

Le document s'ouvre alors à côté du premier et les résultats de la comparaison s'affichent.

.. image:: /_static/images/documentCompare2.png
    :align: center
    :width: 100%

Lancement automatique au démarrage de l'application
---------------------------------------------------

Pour lancer automatiquement la comparaison des documents au démarrage de l'application, utiliser le paramètre : ::
	
	visualization.multiView.doComparison=true

La comparaison ne se lancera que si au moins deux documents sont chargés dans l'applciation.

Le premier document chargé s'ouvrira à gauche et le second à droite.


Comment quitter le mode comparaison ?
=============================

* Pour quitter, cliquer sur la croix présente dans le coin en haut à droite du document à fermer.

.. image:: /_static/images/documentCompare3.png
    :align: center
    :width: 100%

* Il est également possible d'effectuer un clic droit puis de sélectionner \ *Fermer la vue multiple*\ .

.. image:: /_static/images/documentCompare4.png
    :align: center
    :width: 100%


Comment analyser les résultats d'une comparaison ?
==================================================

La couleur d'une ligne définit sa différence avec l'autre document :

+------------------------+-----------------------------------+
|       Couleur          |   Signification                   |
+========================+===================================+
|      Verte             |  Ligne ajoutée                    |
+------------------------+-----------------------------------+
|      Rouge             |  Ligne supprimée                  |
+------------------------+-----------------------------------+
|      Grise             |  Ligne modifiée                   |
+------------------------+-----------------------------------+
|      Orange            |  Modification au sein d'une ligne |
+------------------------+-----------------------------------+

.. image:: /_static/images/documentCompare5.png
    :align: center
    :width: 100%


Comment parcourir les résultats obtenus ?
=========================================

Navigation dans les résultats
-----------------------------

.. image:: /_static/images/documentCompare6.png
    :align: center

Cliquer sur le bouton \ *Résultat suivant*\  ou \ *Résultat précédent*\  redirigera sur le résultat le plus proche, peu importe le document.

.. image:: /_static/images/documentCompare7.png
    :align: center
    :width: 100%

Défilement synchronisé des documents
------------------------------------

Par défaut, lorsqu'une comparaison est effectuée, le défilement synchronisé des documents est actif.

Il est possible de le désactiver en utilisant le bouton correspondant dans le bandeau de navigation.

Correspondance des résultats
----------------------------

Cliquer sur un résultat renvoi à la ligne correspondant à cette différence dans l'autre document. 

.. image:: /_static/images/documentCompare8.png
    :align: center
    :width: 100%


Spécificités du mode comparaison
================================

- Le mode vue multiple intègre un système de document courant, désigné par le dernier par lequel est passé la souris.
  
  C'est ce document qui est pris en compte pour la majorité des fonctionnalités : 
  Annotations, Téléchargement, Impression, Recherche textuelle, Rotation de page ...

- Le changement de document à l'aide des vignettes du volet de navigation est désactivé.

  Seules les vignettes correspondant aux documents ouverts en mode comparaison permettent 
  de changer de page au sein de celui-ci.
  
Comment définir le focus de document par clic
=======================================

Pour définir le focus de document par clic utilisé le paramètre : ::
	
	visualization.multiView.focusOnClick=true
|