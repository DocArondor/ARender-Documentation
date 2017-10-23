Annotations
===========

* Clé: *annotation*

    ==============================================================   =======================  =========
    Description                                                      Clé du paramètre         Type
    ==============================================================   =======================  =========
    Mode de sauvegarde automatique                                   autosave                 Booléen
    Chargement des annotations existantes                            loadExisting             Booléen
    Affichage d'un GIF de chargement à la sauvegarde d'annotations   loadingGIF               Booléen
    Recherche dans le contenu textuel des annotations                searchTextInAnnotations  Booléen
    ==============================================================   =======================  =========

* Exemple ::

    // Activation du mode autosave
    annotation.autosave=true
    // Affichage du GIF de chargement
    annotation.loadingGIF=true
   
Note textuelle
--------------
  
* Clé: *annotation.stickyNote*

    =======================================   ==================   =========
    Description                               Clé du paramètre     Type
    =======================================   ==================   =========
    Opacité                                   opacity              Booléen
    Largeur minimum                           minimum.width        Entier
    Hauteur minimum                           minimum.height       Entier
    Couleur de fond                           default.color        Texte
    Couleur de police                         default.fontColor    Texte
    Taille de police                          default.fontSize     Entier
    Choix de police                           default.font         Texte
    Texte souligné                            default.underline    Booléen
    Texte gras                                default.bold         Booléen
    Texte italique                            default.italic       Booléen
    Cacher la bordure                         hide.border          Booléen
    Cacher les détails de la note textuelle   hide.details         Booléen
    =======================================   ==================   =========
    
Rectangle
------------------
  
* Clé: *annotation.rectangle*

    ======================================  ====================  =========
    Description                             Clé du paramètre      Type
    ======================================  ====================  =========
    Opacité                                 opacity               Décimal
    Largeur minimum                         minimum.width         Entier
    Hauteur minimum                         minimum.height        Entier
    Couleur de fond                         default.color         Booléen
    Couleur de la bordure                   default.border.color  Texte
    Taille de la bordure                    default.border.width  Entier
    ======================================  ====================  =========


Cercle
------------------
  
* Clé: *annotation.circle*

    ======================================  ====================  =========
    Description                             Clé du paramètre      Type
    ======================================  ====================  =========
    Opacité                                 opacity               Décimal
    Largeur minimum                         minimum.width         Entier
    Hauteur minimum                         minimum.height        Entier
    Couleur de fond                         default.color         Booléen
    Couleur de la bordure                   default.border.color  Texte
    Taille de la bordure                    default.border.width  Entier
    ======================================  ====================  =========
    

Texte surligné, souligné et barré
---------------------------------
  
* Clé: *annotation.highligthtext*

    ======================================  ==================  =========
    Description                             Clé du paramètre    Type
    ======================================  ==================  =========
    Opacité                                 opacity             Décimal
    ======================================  ==================  =========


Masquage
--------

    =======================================  =============================   =========
    Description                              Clé du paramètre                Type
    =======================================  =============================   =========
    Autorisation de cacher les masquages     annotation.canHideObfuscate     Booléen
    Protéger les masquages                   toolbar.lockedObfuscate         Booléen
    =======================================  =============================   =========


Polygone
--------
  
* Key: *annotation.polygon*

    ======================================  ====================  =========
    Description                             Clé du paramètre      Type
    ======================================  ====================  =========
    Opacité                                 opacity               Décimal
    Couleur de fond                         backgroundColor       Entier
    Largeur de la bordure                   width                 Décimal
    ======================================  ====================  =========


Ligne connecté
--------------
  
* Key: *annotation.polyline*

    ======================================  ====================  =========
    Description                             Clé du paramètre      Type
    ======================================  ====================  =========
    Opacité                                 opacity               Décimal
    Couleur de fond                         backgroundColor       Entier
    Largeur de la bordure                   width                 Décimal
    ======================================  ====================  =========


Main levée
----------
  
* Key: *annotation.ink*

    ======================================  ====================  =========
    Description                             Clé du paramètre      Type
    ======================================  ====================  =========
    Opacité                                 opacity               Décimal
    Couleur de fond                         backgroundColor       Entier
    Largeur de la bordure                   width                 Décimal
    ======================================  ====================  =========


Flèche
------
  
* Clé: *annotation.arrow*

    =================   ==================   ===================================
    Description         Clé du paramètre     Type
    =================   ==================   ===================================
    Couleur de fond     backgroundColor      String (format RGB ou hexadecimal)
    Mode règle          computeDistance      Booléen 
    =================   ==================   ===================================
    
    
Popup d'information
-------------------

Cette partie concerne l'affichage d'une popup présentant les informations d'une annotation à son survol avec la souris. Cette fonctionnalité a été introduite afin de permettre la consultation des informations d'annotations qui ne sont pas éditables.
  
* Clé: *annotation.info.popup*

    ==========================================================  ==================  =========
    Description                                                 Clé du paramètre    Type
    ==========================================================  ==================  =========    
    Activer / désactiver l'affichage de la popup                enabled             Booléen
    Afficher la popup même si l'annotation est éditable         evenIfEditable      Booléen
    Afficher les informations liées à la dernière mise à jour   displayUpdate       Booléen
    ==========================================================  ==================  =========
    
    
-----------------------------------
Chargement des annotations par page
-----------------------------------

Si le connecteur le supporte par le biais de l'interface *AnnotationPageAccessor*, les annotations peuvent être chargées par page en version 3.1.0 et supérieur.

Voici le paramètre à employer afin d'activer le chargement par page: 

* annotation.loadPerPage=true


La signature de cette interface est la suivante: 

.. code-block:: java

    List<Annotation> get(int page) throws AnnotationsNotSupportedException, AnnotationCredentialsException, InvalidAnnotationFormatException;

Il reste alors au connecteur de faire le travail de cache/accès buffer aux annotations afin de fournir à l'HMI les bonnes annotations.
    