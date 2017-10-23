--------------
API JavaScript
--------------

Configurer un fichier JavaScript personnalisé
=============================================

Le fichier JavaScript personnalisé doit contenir une fonction du type :: 

    function arenderjs_init(arenderjs_){ ... }

Cette fonction est appelée au démarrage d'ARender, l'argument *arenderjs_* est l'objet JavaScript qui collect toutes les API, fournies par ARender.

Votre fichier Javascript peut être configuré pour être utilisé dans ARender de deux façons distinctes : 

Utiliser la propriété arenderjs.startupScript
---------------------------------------------

La propriété arenderjs.startupScript, si elle est définie, sera utilisée par ARender pour récupérer le fichier Javascript personnalisé et l'executer lorsque l'interface sera prête.

Cette propriété peut être définie dans le fichier de profil, ::

    arenderjs.startupScript=scripts/myarenderscript.js
    
Ou directement dans les paramètres URL ::

    http://arender.arondor.com/ARender/ARender.jsp?url=http://arender.arondor.com/pdf/pdf/PDFReference15_v5.pdf&arenderjs.startupScript=scripts/arenderJSPAPITest.js

Ouvrez le fichier *jsapi-demo.properties* (dans le sous-dossier *WEB-INF/classes* du dossier ARender war) pour voir un exemple de profil.
Noter que l'URL JavaScript peut-être fournie :

En tant qu'URL relative: l'URL est relative à "l'ARender HMI context root", par exemple *http://arender.arondor.com/ARender*

En tant qu'URL absolue: dans ce cas, attention la plupart des navigateurs web récents interdisent les requêtes depuis de multiples sources, ce à cause des limitations des XSS.

Le "`Hollywood Principle <https://en.wikipedia.org/wiki/Hollywood_principle>`_ "
------------------------------------------------------------------------------------

L'autre option est de définir la fonction init : *arenderjs_init()* dans ARender dans un contexte parent.
Considérer ARender inclus à une IFrame; L'application appelle l'IFrame à l'aide d'une URL pointant sur ARender.
Dans ce cas, L'application doit définir ::

    function arenderjs_init(arenderjs_){ ... }
    
ARender va lire cette fonction dans un contexte parent, et l'appelle si elle existe.

Utiliser l'API Javascript
=========================

Ouvrir des documents
--------------------

* Objet: arender_js
    +-------------------------------------+--------------------------------------------------------------------------------+
    | Fonction                            | Description                                                                    |
    +=====================================+================================================================================+
    | loadDocument(url , callback)        | Charge un document en fournissant l'URL. La fonction renvoie l'Id ARender.     |
    |                                     | Arguments:                                                                     |
    |                                     |  - L'URL à ouvrir                                                              |
    |                                     |  - Callback pour la fonction à appeler lorsque l'Id est fourni par le serveur. |
    |                                     | Note: Cette opération est uniquement coté serveur, Asynchrone côté client.     |
    +-------------------------------------+--------------------------------------------------------------------------------+
    | openDocument(id)                    | Ouvre un document.                                                             |
    |                                     | Argument:                                                                      |
    |                                     |  - id: L'id d'ARender                                                          |
    +-------------------------------------+--------------------------------------------------------------------------------+
    | askChangePage(type , index)         | Change la page.                                                                |
    |                                     | Arguments:                                                                     |
    |                                     |  - type: 'Relative', 'Index' ou 'Absolute'                                     |
    |                                     |  - index: -1 ou 1 pour relatif ou absolus; sinon le numéro de la page          |
    +-------------------------------------+--------------------------------------------------------------------------------+
    | enablePDFDocumentHyperlinks(booleen)| Active/désactive le chargements des hyperliens natifs du document source.      |
    |                                     | Arguments:                                                                     |
    |                                     |  - booleen : Charge les hyperliens si vrai, ne charge pas(décharge) sinon.     |
    +-------------------------------------+--------------------------------------------------------------------------------+
    | disallowClickOnHyperlinks(booleen)  | Autorise ou non l'ouverture des liens dans ARender pour le document courant    |
    |                                     | Arguments:                                                                     |
    |                                     |  - booleen : bloque la gestion des clique si vrai, l'autorise si faux.         |
    +-------------------------------------+--------------------------------------------------------------------------------+
    

* Exemple ::

    // Loads the PDF reference document
    getARenderJS().loadDocument("http://arender.arondor.com/pdf/pdf/PDFReference15_v5.pdf",
   function(id)
   {
       getARenderJS().openDocument(id);
   });

    // Move to page 24 (note that first page is called 0)
    getARenderJS().askChangePage('Index',23);

    // Move to last page
    getARenderJS().askChangePage('Absolute',1); 


S'abonner aux erreurs de chargement des documents
-------------------------------------------------

* Objet: arender_js

    +---------------------------------------------------+-----------------------------------------------------------------------------------------+
    | Fonction                                          | Description                                                                             |
    +===================================================+=========================================================================================+
    | registerNotifyLoadingErrorEvent(callback)         | Enregistre une fonction callback à appeller en cas d'erreur de chargement des documents |
    |                                                   |                                                                                         |
    |                                                   |  Arguments:                                                                             |
    |                                                   |  - La fonction callback à appeller en cas d'erreur                                      |
    +---------------------------------------------------+-----------------------------------------------------------------------------------------+
    

* Exemple

.. code-block:: javascript

    // Subscribe a function to the errors
    getARenderJS().registerNotifyLoadingErrorEvent(function(documentId,message) {console.log("error: "+message)});
    // Loads the PDF reference document
    // If an error occurs I am notified on the function defined before!
    getARenderJS().loadDocument("http://arender.arondor.com/pdf/pdf/PDFReference15_v5.pdf",
   function(id)
   {
       getARenderJS().openDocument(id);
   });
   
S'abonner à la fin du chargement des modules asynchrones ARender
----------------------------------------------------------------

* Objet: arender_js

    +---------------------------------------------------+-----------------------------------------------------------------------------------------+
    | Fonction                                          | Description                                                                             |
    +===================================================+=========================================================================================+
    | registerAllAsyncModulesStartedEvent(callback)     | Enregistre une fonction callback à appeller en fin de chargement des modules            |
    |                                                   | asynchrones.                                                                            |
    |                                                   |  Arguments:                                                                             |
    |                                                   |  - La fonction callback à appeller à la fin du chargement                               |
    +---------------------------------------------------+-----------------------------------------------------------------------------------------+
    

* Exemple

.. code-block:: javascript
	
	// Subscribe a function to the loading
    getARenderJS().registerAllAsyncModulesStartedEvent(function() {console.log("modules are loaded")});
    // When asynchronous modules are loaded I am notified on the function defined before!



Changer le zoom
---------------

* Objet: getARenderJS().getZoomJSAPI()

    ===================================     ============================================================
    Fonction                                Description          
    ===================================     ============================================================
    askZoomIn()                             Zoomer
    askZoomOut()                            Dézoomer
    askZoomFullWidth()                      Zoomer suivant la largeur maximal de l'écran
    askZoomFullHeight()                     Zoomer suivant la hauteur
    askZoomFullPage()                       Zoomer à la taille la plus adaptée entre hauteur/largeur
    ===================================     ============================================================
        
Changer le découpeur de documents
---------------------------------

* Object: getARenderJS().getDocumentBuilder()

    ===================================     ======================================
    Fonction                                Description          
    ===================================     ======================================
    close()                                 Ferme le découpeur de documents
    open()                                  Ouvre le découpeur de documents
    reset()                                 Remet à zéro le découpeur de documents
    ===================================     ======================================
        
Changer le navigateur de documents
----------------------------------

* Objet: getARenderJS().getThumbnailsJSAPI()

    ===================================     =============================================================================
    Fonction                                Description          
    ===================================     =============================================================================
    resetNavigator()                        Remet à zéro la taille du navigateur de documents
    hideNavigator()                         Cache le navigateur de vignettes
    showNavigator()                      	Montre le navigateur de vignettes
    expandNavigator(width)                  Agrandi le navigateur de vignettes (si la taille est supérieure à l'actuelle)
    reduceNavigator(width)                  Réduit le navigateur de vignettes (si la taille est inférieure à l'actuelle)
    ===================================     =============================================================================
    
Mettre en plein écran
---------------------
    
* Objet: getARenderJS().getFullScreenJSAPI()

    ===================================        ==================================
    Fonction                                   Description          
    ===================================        ==================================
    askOpenFullScreen()                        Active le mode plein écran
    askCloseFullScreen()                       Désactive le mode plein écran
    ===================================        ==================================

Rotation de pages
---------------------    
    
* Objet: getARenderJS().getRotateJSAPI()

    ===================================     ===================================================================================
    Fonction                                Description          
    ===================================     ===================================================================================
    askRotateCurrentPageLeft()              Rotation de la page active sur la gauche (sens inverse des aiguilles d'une montre)
    askRotateCurrentPageRight()             Rotation de la page active sur la droite (sens des aiguilles d'une montre)
    askRotateAllPageLeft()                  Rotation de toutes les pages sur la gauche 
    askRotateAllPageRight()                 Rotation de toutes les pages sur la droite
    ===================================     ===================================================================================
    
Fonctions de recherche
----------------------
    
* Objet: getARenderJS().getSearchJSAPI() 

    ===================================     ========================================
    Fonction                                Description          
    ===================================     ========================================
    askSearchTextNext(word)                 Recherche pour le prochain mot : "word"

                                            Argument: 

                                              - word: Le mot que l'on cherche
    askSearchTextPrevious(word)             Recherche pour le précédent mot : "word"

                                            Argument: 

                                              - word: Le mot que l'on cherche
    clearSearchResults()                    Efface les résultats de la recherche
    ===================================     ========================================

Télécharger des documents
-------------------------
    
* Objet: getARenderJS().getDownloadDocumentJSAPI()  

    ===================================     ================================================================
    Fonction                                Description          
    ===================================     ================================================================
    askDownloadDocumentPDF()                Télécharger le document pdf actif
    askDownloadDocumentSource()             Télécharger le document actif au format source
    askDownloadAllDocuments()               Télécharger un unique pdf regroupant tous les documents ouverts
    ===================================     ================================================================

Intercepter les évenements d'hyperlien
--------------------------------------

* Objet: getARenderJS().getAnnotationJSAPI()

Voici un exemple de code permettant d'enregistrer une méthode qui sera appellée à chaque click sur un hyperlien : 

.. code-block:: javascript
    
    var arenderjs;
    function followLink(docId, pageNumber, destination, action)
    {
        alert("docId=" + docId + ", pageNumber=" + pageNumber + ", dest=" + destination + ", action=" + action);
        alert(arenderjs.getPropertyFromDestination(destination,"PAGE_TARGET"));
        alert(arenderjs.getPropertyFromAction(action,"GOTO"));
    }

    function arenderjs_init(ajs) 
    {
        ajs.onAnnotationModuleReady(function(annotjs)
                {
                    arenderjs=annotjs;
                    annotjs.registerFollowLinkHandler(followLink); 
                    console.log(arenderjs.getDestinationTypes().b);
                    console.log(arenderjs.getActionTypes().b);
                });
    }

Dans cet exemple, vous pouvez également observer comment visualiser toutes les propriétées existantes dans les hyperliens.

*arenderjs.getDestinationTypes().b* et *arenderjs.getActionTypes().b* contiennent la liste des propriétés actuellement gérées par ARender et pouvant être retournées. 

*arenderjs.getPropertyFromDestination(destination,property)* et *arenderjs.getPropertyFromAction(action,property)* permettent de récupérer une propriété souhaitée. 

Voici enfin la liste des propriétés disponibles pour les *destinations* et *actions* .

.. code-block:: java

    
    public static enum DestinationTypes
    {
        PAGE_TARGET, NAMED_DESTINATION, GOTO_DESTINATION, URI, BOTTOM_POSITION, TOP_POSITION, LEFT_POSITION, RIGHT_POSITION, INCORRECT_SYNTAX;
    }

    public static enum HyperlinkActionTypes
    {
        REMOTE_GOTO, LAUNCH, GOTO, NAMED, URI, JAVASCRIPT, NONE, FILE_SPECIFICATION, WIN_LAUNCH_PARAMS, INCORRECT_SYNTAX;
    }

Les actions indiquent quel type de champs vont être trouvé. Un *GOTO* contient une notion de page et peut contenir des coordonnées (retournent -1 si inexistantes), une *URI* va contenir une *URI* en destination etc...


Préparer un événement de lancement de plugin ARender
----------------------------------------------------
 
* Objet: getARenderJS()

    ========================================     =============================================================================================
    Fonction                                     Description          
    ========================================     =============================================================================================
    preparePluginEvent(key,value,pluginName)      Insère un couple (Key,Value) à la future URL du plugin ouvert dans ARender de nom pluginName
    clearPluginEvent(pluginName)                  Nettoie toute valeur potentiellement stockée (Key,Value) au plugin nommé pluginName
    openPlugin(pluginName,openInMultiView)        Ouvre le plugin pluginName dans ARender, en multiView ou non avec le booléen openInMultiView
    ========================================     =============================================================================================
    
Ces fonctions permettent de préparer un événement d'ouverture de plugin afin d'enrichir son lancement de manière contextualisée depuis ARender.

.. code-block:: javascript

    function arenderjs_init(ajs) 
    {
    	// ceci prépare une URL du type http://plumeURL/?To=toto@tutu.com
        ajs.preparePluginEvent("To","toto@tutu.com","plume");
     	// si on ne veut effacer ces valeurs (action sur un bouton clear par exemple)
        ajs.clearPluginEvent("plume");
    }