----------------------------------------
Configuration du serveur de présentation
----------------------------------------

Fichiers présents dans WEB-INF/classes
======================================

(le web-inf/classes utilisé par votre HMI , tomcat, jetty ou websphere)

    ================       ====================================================================================================================================================================================================================
    Nom du fichier         Rôle et Contenu
    ================       ====================================================================================================================================================================================================================
    arender.xml            Configuration principale de l’application ARender HMI incluant l'accès au(x) serveur(s) de rendition et les connecteurs (Cf. `Connecteurs <file:///C:/Users/A.%20BOUAZZAOUI/Desktop/sphinxHTML/connecteurs.html>`_.)
    ehcache.xml            Configuration du cache des documents ouverts via l’interface graphique.
    log4j.properties       Configuration des journaux applicatifs
    Autres fichiers        Configuration des profils utilisateurs (cf. `Guide de configuration <file:///C:/Users/A.%20BOUAZZAOUI/Desktop/sphinxHTML/guide.html>`_)
    ================       ====================================================================================================================================================================================================================


Définition de serveur de rendition
==================================

Afin de définir un ou plusieurs serveurs de rendition, il suffit d'éditer le fichier arender.xml de la manière suivante :

.. code-block:: xml

    <bean id="delegate" class="com.arondor.viewer.common.javarmi.ClientDocumentService" scope="singleton">
        <property name="maxTries" value="5" />
        <property name="remoteTargets">
        <list>
            <value>rmi://{serveur_de_rendition_1}:1789/JavaRMIDocumentService</value>
            <value>rmi://{serveur_de_rendition_2}:1789/JavaRMIDocumentService</value>
        </list>
        </property>
    </bean>



**Nota bene** *: Le contenu de la balise "<value>" ci-dessus est à modifier par l'adresse du serveur de rendition configuré.*

*(ne pas oublier de redémarrer votre HMI)*

Feuille de style : ARender-default.css
======================================

La plupart des composants graphiques d’ARender peuvent être paramétrés dans la feuille de style. Consulter le fichier pour plus de détails.

**Nota Bene** *: Cette feuille de style est liée au profil par défaut. Se référer au Guide de configuration pour plus de détails.*



