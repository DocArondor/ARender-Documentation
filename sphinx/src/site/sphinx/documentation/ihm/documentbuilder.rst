
------------------------
Composition de documents
------------------------

* Clé: documentbuilder
    
    ====================================================================================  ======================   =========
    Description                                                                           Clé du paramètre         Type
    ====================================================================================  ======================   =========
    Activation/désactivation du composant                                                 enabled                  Booléen
    Montrer/Cache le bouton de la composition de documents                                button.visible           Booléen
    Rendre les images du composeur de documents déplaçables (ou non)                      thumbs.draggable         Booléen
    Activation de la composition de document au démarrage                                 activateOnStartup        Booléen
    Cache le navigateur de document                                                       hideDocumentNavigator    Booléen                              
    Largeur                                                                               width                    Pixels
    Comportement de la sauvegarde                                                         save.behavior            Texte
    Télécharger le document après la sauvegarde                                           save.download            Booléen
    Effacer le document après la sauvegarde. Autrement le document est figé/grisé.        save.delete              Booléen
    Afficher une notification quand on quitte la page avec des documents non sauvegardés  displaySaveWarning       Booléen
    ====================================================================================  ======================   =========

* Exemple ::

    // Active la composition de documents. Un document sera créé dans le référentiel d'origine et grisé si la sauvegarde est réussie
    
    documentbuilder.enabled=true
    documentbuilder.save.behavior=CREATE_NEW_FIRST_DOCUMENT
    documentbuilder.save.delete=false

