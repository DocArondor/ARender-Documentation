---------------------------
Installation de wkhtmltopdf
---------------------------

**Méthodologie à suivre pour ajouter le paquet wkhtmltopdf pour l'ouverture d'emails (Distribution Linux uniquement)**

*Nota : Cette étape n’est à réaliser que pour les distributions Linux pour l’ouverture d’emails.*

Gestionnaire de paquets
=======================

Si *wkhtmltopdf* fait partie des paquets disponibles pour la distribution Linux, il suffit de taper la commande suivante :

* Sous RedHat ::

    yum install wkhtmltopdf

* Sous Debian ::

    apt-get install wkhtmltopdf

Installation manuelle
=====================

1. Télécharger *wkhtmltopdf* sur Google Code ::

   wget http://wkhtmltopdf.googlecode.com/files/wkhtmltopdf-0.11.0_rc1-static-amd64.tar.bz2

2. Décompresser l'archive récupérée ::

   tar -xvf wkhtmltopdf-0.11.0_rc1-static-amd64.tar.bz2

3. Déplacer le répertoire *wkhtmltopdf-amd64* ::

   mkdir /product/wkhtmltopdf
   mv wkhtmltopdf-amd64

4. Configurer ARender pour utiliser *wkhtmltopdf* (*arender-rendition.xml*)

   Repérer la propriété *tools.wkhtmltopdf.path* dans le fichier `arender-rendition.properties` et mettre la valeur de votre chemin d'installation.


-----------------------------
Configuration de Libre Office
-----------------------------

**Configuration pour les documents Office :**

Prérequis : Cette étape est à réaliser après l’installation de LibreOffice. Si LibreOffice n’est pas installé sur le poste, veuillez installer LibreOffice à la racine du disque ou dans le répertoire « *Program Files* ».

Pour les versions de l'HMI  inférieures à 3.0
=============================================

Par défaut, ARender Rendition n'est pas configurer pour traiter les documents LibreOffice. Pour rendre cela possible il est nécessaire de :

* Éditer le fichier de configuration « arender-rendition.xml », situé dans le dossier  « conf » du dossier du serveur de Rendition.
* Rechercher le bean « *officeConverter* »
* Décommenter les propriétés « *officeHome* », « *forceShutdownOfficeManager* » et « *delayedOfficeManagerStart* »

Remplacer si nécessaire la valeur de la propriété « *officeHome* » par le chemin du dossier LibreOffice suffixé par « *App\\libreoffice\\* ». C'est le chemin qui contient le dossier « *program* » qui contient lui même le fichier « *soffice.bin* ».

**Exemple :** ::

    <bean id="officeConverter" class="com.arondor.fast2p8.convert.openoffice.OOConvert">
        <property name="tempFolder" value="../tmp/doc/" />
        <property name="supportedSourceMimeTypes">
            <list />
        </property>
        <property name="officeHome" value="C:\LibreOfficePortable\App\libreoffice\" />
        <property name="forceShutdownOfficeManager" value="true"/>
        <property name="delayedOfficeManagerStart" value="5"/>
        <property name="forceStopCommand" value="taskkill /IM soffice.bin /F" />
    </bean>

Ici, le chemin configuré est ::

    C:\LibreOfficePortable-3.5.2\App\libreoffice\

**Ne pas oublier de relancer le service ARender pour que les changements soient pris en compte.**

Pour les versions de l'HMI  supérieures à 3.0
=============================================

Par défaut, ARender Rendition n'est pas configurer pour traiter les documents LibreOffice, Pour rendre cela possible il est nécessaire de :

* Éditer le fichier de configuration « arender-rendition.xml », situé dans le dossier  « conf » du dossier du serveur de Rendition.
* Rechercher le bean « **cmdlineOfficeFactory** ».
Remplacer la valeur « *soffice* » de la propriété « *officePath* » par le chemin de d'installation de LibreOffice, suffixé par « *\App\libreoffice\program\soffice.exe* ». Il s'agit du chemin permettant d'executer le fichier « *soffice.exe* ».

* **Exemple :** ::

    <bean id="cmdlineOfficeFactory" class="com.arondor.viewer.rendition.office.LibreOfficeCommandLineConverter">
       <property name="officePath" value="E:\Program Files\LibreOfficePortable\App\libreoffice\program\soffice"/>
       <property name="outPath" value="../tmp/doc"/>
       <property name="officeOptions">
       <list>
            <value>--headless</value>
            <value>--convert-to</value>
            <value>pdf:writer_pdf_Export</value>
       </list>
       </property>
    </bean>

Ici le chemin configuré est ::

    E:\Program Files\LibreOfficePortable\App\libreoffice\program\soffice

**Ne pas oublier de relancer le service ARender pour que les changements soient pris en compte.**


---------------------
La vidéo dans ARender
---------------------

La vidéo fait désormais partie d'ARender depuis la version 3.1.0!

Les formats supportés dépendent fortement des navigateurs, et pour l'instant tout format vidéo autre que mp4 sera converti par ARender avant de l'afficher. (Attention: une conversion vidéo prend beaucoup plus de temps qu'un simple parsing d'une video MP4)

La liste des formats de vidéo codec supportés nativement par ARender sont:

- H.264 et MP3 dans un conteneur MP4 (support IE9+, Chrome, Firefox, Opera)
- H.264 et AAC (format cible de conversion pour ARender) dans un conteneur MP4 (support IE9+, Chrome, Firefox, Opera)

Configuration
=============

Il est nécessaire de laisser l'installeur choisir ffmpeg, les chemins sont configurés de base pour une utilisation de ce module embarqué. S'assurer que l'utilisateur pourra lancer les programmes ffmpeg et ffprobe contenus dans le dossier ffmpeg-windows/bin/ ou ffmpeg-linux/ de la rendition.

Il est possible d'ajouter dans le arender-rendition.xml des formats de fichier vidéo dans la liste des factories.

.. code-block:: xml

    <entry>
        <key>
            <value>video/quicktime,(insérer les autres formats ici)</value>
        </key>
        <ref bean="videoConversionFactory" />
    </entry>


Pour le moment nous n'avons intégré que le quicktime à des fins de démonstration. Comme la conversion de vidéo est coûteuse en CPU nous préféreront laisser la configuration au choix de l'intégrateur. Il est nécessaire de garder à l'esprit que des conversions vidéo nécessiteront un dimensionnement particulier du serveur de rendition.

--------------------------------------------------
Configurer le remplacement des documents en erreur
--------------------------------------------------

ARender permet de choisir un document à remplacer en cas d'erreur. Ce document doit être configuré côté Rendition dans le fichier arender-rendition.xml .


Configuration :
===============

Enlever les commentaires sur les properties *rejectedDocumentsPath* et *rejectedDocumentReplacement*, afin que votre XML corresponde à ceci:

.. code-block:: xml

    <!-- Copy all documents with errors to the rejected path -->
    <property name="rejectedDocumentsPath">
        <value>${rendition.dir.rejected.documents}</value>
    </property>
    <!-- Replace all documents with errors by a static image -->
    <property name="rejectedDocumentReplacement">
        <bean class="com.arondor.viewer.rendition.image.StaticImageDocumentModel">
            <property name="title" value="Error"/>
            <property name="imagePath" value="${default.rejected.file}"/>
            <property name="pageDimensions">
                <bean class="com.arondor.viewer.client.api.document.PageDimensions">
                    <constructor-arg value="1600"/>
                    <constructor-arg value="1312"/>
                    <constructor-arg value="0"/>
                </bean>
            </property>
        </bean>
    </property>

Il est alors possible de configurer le *default.rejected.file* dans arender-rendition.properties ainsi que le *rendition.dir.rejected.documents*.

- *default.rejected.file* correspond au fichier image à charger.
- *rendition.dir.rejected.documents* correspond au dossier dans lequel les fichiers en erreur vont se retrouver.

------------------------------------------
Configurer Aroms2pdf pour Microsoft Office
------------------------------------------

Introduction
============

ARender permet également d'utiliser Microsoft Office pour la prise en charge des documents Office.

Pré-requis :
============

.Net 4.5 : http://www.microsoft.com/fr-fr/download/details.aspx?id=30653

Microsoft Visual C++ redistributable 2010 : https://www.microsoft.com/fr-fr/download/details.aspx?id=14632

Microsoft Visual C++ redistributable 2008 : https://www.microsoft.com/en-us/download/details.aspx?id=15336


Création des dossiers système :
===============================

C:\\Windows\\System32\\config\\systemprofile\\Desktop

C:\\Windows\\SysWOW64\\config\\systemprofile\\Desktop

Installation
============

**Paramétrage lors de l'installation du serveur de rendition**

Il suffit ici de cocher la case à cocher Aroms2pdf bundle for Windows

.. image:: /_static/images/Installation-aroms2pdf_imagelarge.png
    :align: center

Configuration :
===============

Import du fichier xml :
-----------------------

arender-windows.xml : Rajouter la ligne après le premier <import.. ::

<import resource="arender-rendition-aroms2pdf.xml" />

Changement de la Factory :
--------------------------

* Pour les version 2.3.8 minimum et inférieures à 3.1.0

Remplacer dans **arender-rendition.properties** :

 *rendition.backend.msword=officeFactory* par *rendition.backend.msword=aroms2pdfFactory*


Pour les versions **2.3.5 minimum à 2.3.7 maximum**

Remplacer dans arender-rendition.xml :

.. code-block:: xml

    <!-- Microsoft Office Word formats -->

    <entry>
        <key>
            <value>text/rtf,application/msword,application/vnd.openxmlformats-officedocument.wordprocessingml.document</value>
        </key>
        <ref bean="officeFactory" />
    </entry>

par :

.. code-block:: xml

    <!-- Microsoft Office Word formats -->

    <entry>
        <key>
            <value>text/rtf,application/msword,application/vnd.openxmlformats-officedocument.wordprocessingml.document</value>
        </key>
        <ref bean="aroms2pdfFactory" />
    </entry>


Pour les versions **supérieures à 3.1.0** :

Changez les propriétés dans le fichier arender-rendition.properties :

  rendition.backend.msword=cmdlineOfficeFactory en **aroms2pdfFactoryWord**

  rendition.backend.msexcel=cmdlineOfficeFactory en **aroms2pdfFactoryExcel**

  rendition.backend.mspowerpoint=cmdlineOfficeFactory en **aroms2pdfFactoryPowerpoint**

Lancez la rendition dans un compte utilisateur - administrateur ou non - (Services > ARender Rendition Service > Connexion) **avec lequel Microsoft Office s'ouvre sans soucis ni pop-ups**. Les pop-ups empêchent le bon fonctionnement d'Office et donc de notre rendition pilotée.

Pour la configuration des conversions de fichiers Excel, pensez à vérifier que votre utilisateur possède également une imprimante par défaut configurée et fonctionnelle (par exemple, conversion vers XPS) afin de pouvoir faire des opérations de travail sur les pages des feuilles Excel.

------------------------------------------------------
Autoriser la rendition à accéder au système de fichier
------------------------------------------------------


Pour des raisons de sécurité la rendition n'a pas accès à tout le système de fichier.

Afin d'ajouter des chemins il suffit de modifier la propriété *localFileBasePaths* du fichier *arender-rendition.xml*.


.. code-block:: xml

		<property name="localFileBasePaths">
			<list>
				<value>../samples</value>
        <value>votre chemin de fichier ici</value>
        <value>un autre chemin que vous souhaitez ajouter</value>
        <value>etc...</value>
			</list>
		</property>
