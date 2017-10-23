Where to place your custom XML integration
==========================================

We possess in ARender two folders dedicated to custom integrations that ship out empty in order for integration to include easier custom XML into ARender. Those two XML files are imported by ARender. 

This avoid conflicts on version upgrade of ARender, and facilitates the comparison with the new version of the XML (nothing new is overriden by custom integration). 

Those XML files are empty and will always be at each new version. 

In the rendition server:
        - conf/arender-rendition-custom-integration.xml
In the HMI:
        - WEB-INF/classes/arender-custom-integration.xml (GUI, client side configuration)
        - WEB-INF/classes/arender-custom-server-integration.xml (server side configuration)

