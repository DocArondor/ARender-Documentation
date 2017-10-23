--------------------------------
Prérequis - Serveur de rendition
--------------------------------

Liste des prérequis nécessaires à l'installation d'ARender

Serveur de rendition
====================

Configuration matérielle requise :
----------------------------------

        ===========        =================      ================================================================================================
        Catégorie          Minimum                Conseillé
        ===========        =================      ================================================================================================
        Nb Serveur         1                      2 (Haute disponibilité)
        RAM                4Go                    8Go
        CPU (vCPU)         4                      8
        Type de CPU        64Bits                 64Bits
        Stockage           10Go                   Le maximum entre 10Go et une capacité permettant de stocker une journée de documents temporaires
        ===========        =================      ================================================================================================


Configuration matérielle requise :
----------------------------------

        ======================================      ========================================================================================================================================================================================================================================================================================================================================================
        Catégorie                                   Pré-requis
        ======================================      ========================================================================================================================================================================================================================================================================================================================================================
        Système d'exploitation : Windows            Windows 2003 Server ou supérieur
        (ou) Système d'exploitation : Linux         Noyau 2.6 ou supérieur Distributions validées : RedHat (6.4), CentOS (6.5), Debian (7), Ubuntu (10.10), Amazon Linux AMI (2016.09)
        Runtime Java                                JRE 1.7 64 bits Minimum, JDK conseillé Le JDK contient en plus de la JRE les outils d’administration à distance jconsole et jvisualvm. Les JRE OpenJDK et Oracle sont préconisées, la JRE IBM J9 est non supportée. Attention : l'utilisation d'un version java 1.8.x nécessite de renseigner le chemin complet vers la JVM dans le fichier wrapper.conf
        LibreOffice                                 LibreOffice 4.4.3.2 et supérieur conseillé. Attention sur RHEL/CentOS l'installation de LibreOffice 5 nécessite la présence de la librairie libGL.so.1.
        ImageMagick (Linux uniquement)              ImageMagick 6.6.0 ou supérieur
        WKHtmlToPdf (Mail ou HTML)                  wkhtmltopdf 0.12.3.2 (windows) 0.12.3 (Linux)
        ======================================      ========================================================================================================================================================================================================================================================================================================================================================


**Attention : Le serveur de rendition vérifie désormais que la JVM est 64 bits et va s'arrêter sinon. Cette erreur pourra se lire dans le wrapper.log ou la console selon le mode de démarrage de la rendition.**

Autres pré-requis :
-------------------

        ===================        ================================================================================================================================================================================
        Catégorie                  Pré-requis
        ===================        ================================================================================================================================================================================
        Droits utilisateurs        Les droits d’administration suffisants pour la mise en service (Windows ou Linux)
        Firewall                   Ouverture des ports supérieurs à 1024 pour le(s) serveur(s) de présentation (communication via le protocole RMI) Le serveur de Rendition utilise par défaut les ports suivants :
                                    * 1789 : Port RMI d'écoute
                                    * 1889 : Port JMX pour JConsole/JVisualVM
        ===================        ================================================================================================================================================================================
