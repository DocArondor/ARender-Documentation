.. image:: /_static/images/titre-faq.png

.. _FAQ:

==================
FAQ
==================

**Provide answers to frequently asked questions**

--------------------------
How to define another JVM?
--------------------------

According to some contexts, a specific JVM may be used for ARender execution.

For this purpose, the wrapper.conf configuration file must be modified. This files can be found in conf folder of the installation repository (by default: *C:\Program Files\ARender*).

* Locate following lines: ::

    # Locate the java binary on the system PATH:
    wrapper.java.command=java
    # Specify a specific java binary:
    # set.JAVA_HOME=C:\Program Files\Java\jre7
    # wrapper.java.command=%JAVA_HOME% /bin/java

* Modify these lines as follow: ::

    # Locate the java binary on the system PATH:
    # wrapper.java.command=java
    # Specify a specific java binary:
    set.JAVA_HOME=<strong>C:\Program Files\Java\jre7</strong>
    wrapper.java.command=%JAVA_HOME% /bin/java

*The java executable path must be modified according to target environment.*

-------------------------------
How to purge web browser cache?
-------------------------------

After a new installation, it’s possible client side (users) keep in cache another version and that can cause an incompatibility problem with the new ARender HMI application  installed.

The compatibility problem usually solve itself after 24h maximum when browser cache expires.

To solve the problem immediately, all you need is to purge the user browser cache.

**Internet Explorer 6**

-          Click on « Tools » then «  Internet options »

-          In the part « Temporary internet files », click on « delete the files»

-          Check the box « Delete all content off-line », then click on « OK »

**Internet Explorer 9**

-          Click on « Tools » then « Internet Options »

-          Int the part « navigation history », click on « Delete »

-          Check the box « Temporary internet files », then click on « Delete »

*Nota : This problem comes from applications conception in GWT framework which use a specific resource at loading step called  « arendergwt.nocache.js ». The mention ‘.nocache.’ would have to force the browser to not use the cache for this file , but it’s not really respected by Internet Explorer*


---------------------------
Where can I find log files?
---------------------------

Log files trace information and errors about ARender use.

Rendition server
================

To have access to logs, go to « logs » folder of Rendition server installation (by default : « C:\Program Files\ARender-Rendition-2.0.3\logs »)

WebSphere
=========

To have access to ARender application logs, go to « logs » folder of WebSphere installation folder

By default: *« C:\Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\logs »*)

FileNet CE logs are located by default in :

*« C:\Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\FileNet\server1 »*)

--------------------------------------------------------
How can I receive incoming RMI calls through a firewall?
--------------------------------------------------------

In some environments where a certain security level is required, the use of ports may be restricted by a firewall.

The minimal configuration of rendition server, a RMI URI, defines the port of RMI registry. By default, the presentation server (RMI client) asks to this registry in order to obtain a service to communicate with on a random port.

To force the communication on only one port, it is enough to modify a configuration parameter of the rendition server:

* Edit the file: *arender-windows.xml* (or *arender-linux.xml*)

* Modify the *exportDocumentServiceOnRegistryPort* property value by *true*

Example ::

    <bean id="server" class="com.arondor.viewer.rendition.javarmi.Server">
        <property name="registerString" value="rmi://{rendition_server}:1789/JavaRMIDocumentService" />
        <property name="exportDocumentServiceOnRegistryPort" value="true" />
    </bean>

---------------------------------
Which file types can I visualize?
---------------------------------

Using ARender, you are able to visualize many types of file as :

Standard :

* PDF - all versions

* Images : JPEG, PNG, TIFF, GIF, BMP, JNG, PBM, PSD, EPS, PS, DCM (Format DICOM) and `all formats supported by ImageMagick <http://www.imagemagick.org/script/formats.php>`_

* Microsoft Office (97-2013) : Word (.doc, .docx) , PowerPoint (.ppt, .pptx), Excel (.xls, .xlsx), WordML (.xml), Vision (.vsd)

* Composite files:  ZIP, EML, MSG

* Others : TXT, OpenDocument (LibreOffice or OpenOffice)

En option :

* `AFP <http://afpcinc.org/>`_

* AutoCAD DWG

-------------------------
ARender's versions policy
-------------------------

ARender's version policy is set the following way : ::

    [Generation Version].[Major Version].[Minor Version]

Optionally , a packaging version may be introduce, as follow : ::

    [Generation Version].[Major Version].[Minor Version]<span style="font-size: 1.1em;">-[Packaging Version]</span>

*Each number indicate :*

* Generation version : Generation means technological choices, it's an important change from the previous generation.
* Major Version : Each major version provide APIs and interface changes, as well as important new functions.
* Minor Version : Each minor version provide anomalies corrections as well as additional function, disable by default.
* Packaging Version : Each packaging version only provide configuration / default parameters changes, without product's code changes.

**Examples :**

Majors and Minors versions : Major version 2.3.0 has been published the 18/06/2014, and introduced Annotation APIs and JavaScript Api changes.

Packaging and Minor version : Minor version 2.3.5 has been published the 28/01/2015, and version 2.3.5-1 has been published the 02/02/2015.

**Publication rhythm**

A major version is published each year, late june.

This version may also increment the generation version
2015 will see a new product generation, ARender 3.0.

A new minor version is published every six weeks.
Packaging version are on a need basis or if asked.

**Ascending compatibility**

Every three minor versions of the same major release are retro-compatible. This is true for :

* Specifics parameters on server or client side.
* Specific development on various APIs
* Presentation (HMI) and rendition server interoperability

This means majors version can have significant change that will require upgrade of the various ARender's modules.

**Product's support**

Arondor will support every minor versions of the last two major versions,  it's all version from the last two years.

--------------------------------------------
How to set produced image's quality and size
--------------------------------------------

Most documents are being converted inside ARender to be visualized on the browser.

This conversion (rendition) has multiple advantages :

* Streaming : only visualized pages are sent to the client

* Band width reduction : Most produced images' size are smaller than the source.

* Quality : Work being done on the server side, restitution quality doesn't depend on the browser setting (font, graphic hardware, ...).

Most fullscreen pages are about 100ko (un example ici).

Complicated images may be much heavier (scan documents, photos).
On `this document <http://arender.fr/ARender/ARender.jsp?url=http://www.arender.fr/pdf/pdf/Aquarama038.pdf>`_, we are closer to 900ko.
It will also depend on scree resolution : a 1600x900 screen resolution will require a 1300 pixels wide in fullscreen.

ARender's default configuration is conservative quality wise, it works for most documents. However there is no miracle.
**To be clear, there is always the need to make choices between quality and size the images produced.**

On ARender's side, the entire configuration is made on the rendition server, on the arender-rendition-{unix|windows}.xml, bean "jnipdfRenderer". to be precise.
Six main parameters can be used to tip the scale, following are the default values: ::

    <property name="**pageImageMimeType**" value="image/jpeg" />
    <property name="**quality**" value="100"/>
    <property name="**overZoom**" value="1.0"/>
    <property name="**maxWidth**" value="8192"/>
    <property name="**antiAlias**" value="8"/>
    <property name="**imageType**" value="IMAGE_TYPE_RGB"/>

In details :
* **pageImageMimeType** : Image type produced. Can be :

    - image/jpeg : Very effective for scanned documents and pictures
    - image/png : More effective for text document (word, txt, pdf).

Summary:

.. image:: /_static/images/png_vs_jpeg_medium.png
    :align: center

* **quality** : image compression level, jpeg or png (1-100), default is 100.
Grain and compression levels depend on the generated image's type.
Maximal quality is selected by default.

* **overZoom** : Zoom level for the expected zone (float : 0.1 - 2.0, par défaut : 1.0)
Two examples :

    - The 0.8 value imply a 80% zoom on the produced image, If the client is asking for a 1000 pixels wide image, rendition server will produced a 800 pixels wide image, the browser will have to zoom-in at 1000 with the following loss of quality.

    - The 1.2 value will apply a 120% zoom on the produced image, therefor the image will be bigger than necessary. With the rise of new sub-pixelling screens, this option may be interesting to improve image.

* **maxWidth** : Maximum size for images to produced (in pixels). It's especially important for big paper documents (A0 plans for example), when the user zoom-in.

* **antiAlias** : Text rendition needs anti-aliasing, via sub-pixelling technique.

* **imageType** : Produced image's colorspace, choose from :

    - IMAGE_TYPE_RGB

    - IMAGE_TYPE_ARGB

    - IMAGE_TYPE_ARGB_PRE

    - IMAGE_TYPE_BGR

    - IMAGE_TYPE_GRAY

    - IMAGE_TYPE_BINARY

    - IMAGE_TYPE_BINARY_DITHER
