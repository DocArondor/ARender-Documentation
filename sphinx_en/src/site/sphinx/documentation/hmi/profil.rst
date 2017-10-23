========
Profiles
========

**Supplied profiles**

ARender is delivered with a default configuration and three profiles as follows: 

    ===================================        ================================================================================
    Nom                                        Description          
    ===================================        ================================================================================
    Base : arender-default.properties          Default configuration file offering a standard configuration for standalone use
    arender                                    Default profile for standard viewing
    book                                       Profile allowing visualization as book reading
    jsapi-demo                                 Profile presenting all features available with the ARender Javascript API
    ===================================        ================================================================================

* Example ::

    Use of specific profil
    http://arender.arondor.com/ARender/ARender.jsp?url=../samples/arender-en.pdf&props=book

**Add a profile**

In order to add a new profile, it is recommended to create a new file based on default one (arender.properties) placed in WEB-INF\classes folder of the web application to deploy. Then, you simply need to modify it according to this guide.
    