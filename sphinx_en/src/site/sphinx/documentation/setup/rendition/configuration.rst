-----------------
wkhtmltopdf setup
-----------------

**Methodology to follow to add the package wkhtmltopdf, to emails opening (Linux only)**

*This step is only necessary for Linux server to emails opening.*

Using package manager
=====================

If *wkhtmltopdf* is part of packages available for Linux distribution, all you need is to use the following command: ::

* RedHat ::

    yum install wkhtmltopdf

* Debian ::

    apt-get install wkhtmltopdf

Manuel
======

1. Download wkhtmltopdf from Google Code (you may want to check for a newer version and adapt the commands) ::

    wget http://wkhtmltopdf.googlecode.com/files/wkhtmltopdf-0.11.0_rc1-static-amd64.tar.bz2

2. Unzip the downloaded file ::

    tar -xvf wkhtmltopdf-0.11.0_rc1-static-amd64.tar.bz2

3. Move the folder wkhtmltopdf-amd64 ::

    mkdir /product/wkhtmltopdf
    mv wkhtmltopdf-amd64

4. Configure ARender to use wkhtmltopdf* (*arender-rendition.xml*)

* Find property *tools.wkhtmltopdf.path* in `arender-renditions.properties` and put in your installation path.

---------------------------
Libre Office Configuration
---------------------------

**Configuration needed to use office documents :**

Requirements : This step has to be done after the LibreOffice installation. If LibreOffice is not installed on the computer. Please, proceed to the installation at disk root or in « Program Files » folder.

For Rendition versions lower than 3.0
=====================================

By default, ARender is not configured for Office documents rendition. To make it possible it is necessary to :

* Edit configuration file « arender-rendition-windows.xml » located in folder of ARender rendition configuration
* Find bean « officeConverter »
* Uncomment properties « officeHome », « forceShutdownOfficeManager » and « delayedOfficeManagerStart »
Replace if necessary, the value of « officeHome » property by LibreOffice installation folder path, suffixed by « App\libreoffice\ ». This is the path of the folder which contains the folder « program » which contains the file « soffice.bin ».

**Example :** ::

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

Here, the configured path is : ::

    C:\LibreOfficePortable-3.5.2\App\libreoffice\

**Remember to restart ARender service**

For Rendition versions superior than 3.0
========================================

By default, ARender is not configured for Office documents rendition. To make it possible it is necessary to :

* Edit configuration file « arender-rendition-windows.xml » located in folder of ARender rendition configuration
* Find bean « **cmdlineOfficeFactory** »
Replace if necessary, the value of « *officeHome* » property by LibreOffice installation folder path, suffixed by « \App\libreoffice\program\soffice.exe  ». This is the path which permit to execute the file « *soffice.bin* ».

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

Here, the configured path is ::

    E:\Program Files\LibreOfficePortable\App\libreoffice\program\soffice

**Remember to restart ARender service**

------------------------
Video viewing in ARender
------------------------

Video formats are now handled by ARender since version 3.1.0!

Supported formats depends heavily on browsers support, therefor every different format than MP4 will be converted in the rendition server before display. (Warning: a video conversion is much longer than a simple parsing of an MP4 video)

The list of video formats natively supported and displayed without conversion is the following :

- H.264 and MP3 in an MP4 container (IE9+, Chrome, Firefox, Opera)
- H.264 and AAC (target format of ARender video conversion) in an MP4 container (IE9+, Chrome, Firefox, Opera)

Configuration
=============

In order to have video parsing/conversion it is mandatory to have selected ffmpeg in the rendition setup, pathes are also configured by default to use this module out of the box. Ensure that the user running the rendition is able to execute both ffmpeg and ffprobe in the folder ffmpeg-windows/bin/ or ffmpeg-linux/ of the rendition server.

It is possible to add more format that can be converted in the arender-rendition.xml file under the factories map:

.. code-block:: xml

    <entry>
        <key>
            <value>video/quicktime,(insert other formats here)</value>
        </key>
        <ref bean="videoConversionFactory" />
    </entry>


For now, only quicktime (.mov) videos are handled for conversion demonstration purposes but as many can be added as long as ffmpeg supports them. Keep in mind that converting video formats is heavily CPU intensive and rendition servers should be correctly sized for it.


------------------------------------------------------------
Configure ARender feature of erroneous documents replacement
------------------------------------------------------------

ARender allows a document replacement feature in case of errors instead of showing the exception to the end user. This document must be configured in the XML file arender-rendition.xml.


Setup
=====

Remove the comments on the properties *rejectedDocumentsPath* and *rejectedDocumentReplacement*, so that your XML looks like so:

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

It is then possible to configure *default.rejected.file* and *rendition.dir.rejected.documents* in arender-rendition.properties.

- *default.rejected.file* tells which image picture ARender needs to load when an error occur.
- *rendition.dir.rejected.documents* setup the folder path where erroneous documents are placed.

--------------------------------------------
Aroms2pdf configuration for Microsoft Office
--------------------------------------------

Introduction
============

ARender is able to use Microsoft Office for office's documents.

Pre-requisite
=============

.Net 4.5 : https://www.microsoft.com/en-us/download/details.aspx?id=30653

Microsoft Visual C++ redistributable 2010 : https://www.microsoft.com/en-US/Download/confirmation.aspx?id=14632

Microsoft Visual C++ redistributable 2008 : https://www.microsoft.com/en-us/download/details.aspx?id=15336


System folder creation
======================

C:\\Windows\\System32\\config\\systemprofile\\Desktop

C:\\Windows\\SysWOW64\\config\\systemprofile\\Desktop

Installation
============

**Setting during the installation of the rendition server**

Tick the check box for Windows bundle Aroms2pdf

.. image:: /_static/images/Installation-aroms2pdf_imagelarge.png
    :align: center

Configuration
=============

arender-windows.xml : Add this line after the first <import.. ::

    <import resource="arender-rendition-aroms2pdf.xml" />

For versions **lower than 3.1.0** :

arender-rendition.xml : You need to switch:

.. code-block:: xml

    <!-- Microsoft Office Word formats -->

    <entry>

            <key>

                <value>text/rtf,application/msword,application/vnd.openxmlformats-officedocument.wordprocessingml.document</value>

            </key>

        <ref bean="officeFactory" />
    </entry>

for

.. code-block:: xml

    <!-- Microsoft Office Word formats -->

    <entry>

      <key>

        <value>text/rtf,application/msword,application/vnd.openxmlformats-officedocument.wordprocessingml.document</value>

      </key>

      <ref bean="aroms2pdfFactory" />
    </entry>


For versions **higher than 3.1.0** :

Change the following properties in the file arender-rendition.properties according to what types of file you want to handle with Microsoft Office :

rendition.backend.msword=cmdlineOfficeFactory by **aroms2pdfFactoryWord**

rendition.backend.msexcel=cmdlineOfficeFactory by **aroms2pdfFactoryExcel**

rendition.backend.mspowerpoint=cmdlineOfficeFactory by **aroms2pdfFactoryPowerpoint**

Launch the rendition service using a local account - Administrator or not - (Services > ARender Rendition Service > Log On) **with which account Microsoft Office can be opened without issues or pop-ups**. Pop-ups will hinder the piloted mode of Microsoft Office and will block the rendering process of the rendition server.

In order to configure Excel file conversion, please verify that the user launching Excel has also a default printer configured (as an example, the default printer that outputs XPS files) otherwise Excel won't be able to do its work on pageSetup and won't convert the documents.

------------------------------------------------
Allow file system access to the rendition server
------------------------------------------------

For security reasons, the rendition server does not possess a full access to the file system.

In order to allow more paths, the property *localFileBasePaths* of the file named *arender-rendition.xml* must be modified.


.. code-block:: xml

		<property name="localFileBasePaths">
			<list>
				<value>../samples</value>
        <value>add your path here</value>
        <value>yet another added path</value>
        <value>etc...</value>
			</list>
		</property>
