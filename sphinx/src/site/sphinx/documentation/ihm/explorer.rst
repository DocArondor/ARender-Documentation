----------------------
Navigateur de document
----------------------

* Clé: documentnavigator

    =================================   =================   ===========
    Description                         Clé du paramètre    Type    
    =================================   =================   ===========
    Largeur du navigateur de document   width               Pixels
    =================================   =================   ===========

Explorateur de vignettes
========================

Le tableau ci-dessous présente la configuration générale de cet explorateur.


* Clé: thumbexplorer


    =======================================================         =================   ===========
    Description                                                     Clé du paramètre    Type    
    =======================================================         =================   ===========
    Activation/désactivation de cet explorateur                     enabled             Booléen
    Indentation entre un document fils et son père                  indentation         Pixels
    Niveau de profondeur de sous documents à charger                maxLevelToLoad      Entier
    Activation/désactivation de l'affichage de métadonnées          metadata            Booléen
    =======================================================         =================   ===========
    
* Exemple ::

    // Désactivation de l'onglet correspondant à l'explorateur de vignettes
    thumbexplorer.enabled=false


Le tableau ci-dessous présente la configuration liée aux vignettes.


* Clé: thumbexplorer.thumb


    ==========================================================================          =================   ===========
    Description                                                                         Clé du paramètre    Type    
    ==========================================================================          =================   ===========
    Largeur des vignettes                                                               width               Pixels
    Marge entre chaque vignette                                                         margin              Pixels
    Largeur de l'explorateur à partir de laquelle les vignettes s'élargissent           grow.min            Pixels
    Incrément d'élargissement des vignettes                                             grow.increment      Pixels
    NA                                                                                  grow.ratio          Entier
    ==========================================================================          =================   ===========

* Exemple ::

    // Définition d'un explorateur dont les vignettes s'agrandissent lorsqu'il est agrandi par l'utilisateur
    thumbexplorer.thumb.width=100
    thumbexplorer.thumb.margin=200
    thumbexplorer.thumb.increment=10

Explorateur d'annotations
=========================

* Clé: annotationexplorer


    ======================================================  =====================   ===========
    Description                                             Clé du paramètre        Type    
    ======================================================  =====================   ===========
    Activation de l'affichage de l'onglet de l'explorateur  enabled                 Booléen
    Affichage des réponses de note textuelle                showStickyNoteReplies   Booléen
    Affichage du label Note textuelle avant le contenu      showStickyNoteLabel     Booléen
    Adaptation de l'explorateur à la taille du tableau      adaptiveWidth.enabled   Booléen
    ======================================================  =====================   ===========


* Exemple ::

    annotationexplorer.enabled=false
    annotationExplorer.showStickyNoteReplies=false
    annotationExplorer.showStickyNoteLabel=true
    annotationExplorer.adaptativeWidth.enabled=false

Explorateur de signets
======================

* Clé: bookmarkexplorer


    ============================================   =================   ===========
    Description                                    Clé du paramètre    Type
    ============================================   =================   ===========
    Activation/désactivation de cet explorateur    enabled             Booléen
    ============================================   =================   ===========


* Exemple ::

    // Désactivation de l'onglet correspondant à l'explorateur de signets
    bookmarkexplorer.enabled=false

