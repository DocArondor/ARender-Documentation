-------------------------------
Requirements - Rendition server
-------------------------------

Minimal hardware
----------------

        =============================   =================   ========================================================================================
        Category                        Minimum             Advised
        =============================   =================   ========================================================================================
        Number of rendition server(s)   1                   2 (for high availability)
        RAM                             4Go                 8Go
        CPU (vCPU)                      4                   8
        CPU type                        64Bits              64Bits
        Storage                         10Go                The maximum between 10Go and a storage where a full day of temporary files can be stored
        =============================   =================   ========================================================================================

Software requirement
--------------------

        ===================================     ======================================================================================================================================================================================================================================================================================
        Category                                Pre-requisite
        ===================================     ======================================================================================================================================================================================================================================================================================
        Operating system : Windows              Windows 2003 Server or higher
        (or) Operating system : Linux           Kernel 2.6 or higher, Validated Distributions : RedHat (6.4), CentOS (6.5), Debian (7), Ubuntu (10.10), Amazon Linux AMI (2016.09)
        Runtime Java                            JRE 1.7 64 bits Minimum, JDK advised, JDK also allow the use of remote administrative tools : *jconsole* and *jvisualvm*. JRE OpenJDK and Oracle are desirable, JRE IBM J9 is unsupported. Note: using java 1.8.x requires to set the absolute path of java in the 'wrapper.conf' file
        LibreOffice                             LibreOffice 4.4.3.2 and up is advised. Warning: LibreOffice 5 on RHEL/CentOS requires libGL.so.1.
        ImageMagick (Linux only)                ImageMagick 6.6.0 or higher
        WKHtmlToPdf (Mail or HTML)              wkhtmltopdf 0.12.3.2 (windows) 0.12.3 (Linux)
        ===================================     ======================================================================================================================================================================================================================================================================================

* Warning :

If the JVM used is not 64 bits, the rendition will now stop its boot and warn in the wrapper.log/console that the version of the JVM used is incorrect.


Other pre-requisite
-------------------

        ===================    ======================================================================================================
        Category               Pre-requisite
        ===================    ======================================================================================================
        User rights            Admin rights are enough to install the service (Windows or Linux)
        Firewall               Ports higher than 1024 need to be open for the presentation servers (communication via RMI protocole)
                               Ports used by rendition server :

                                    * 1789 : RMI listening port
                                    * 1889 : JMX port for JConsole/JVisualVM
        ===================    ======================================================================================================
