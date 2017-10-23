Add new image/video mime types
==============================

If your rendition server does not possess all the mime types that you wish to use, it is then still possible that the rendition server could convert your file.

In the specific case of video/image conversion, the full list of files that can opened by imagemagick/ffmpeg is long. 

If you wish to add this mime type, just modify the *arender-rendition.xml* file of the conf/ folder of the rendition server.  

As an example, if you wish to add the mime type *image/x-bmp* : 

.. code-block:: xml

	<property name="factories">
		...
		<entry>
			<key>
				<value>image/png,image/jpeg,image/gif</value>
			</key>
			<ref bean="imageFactory" />
		</entry>	
		
Would become : 

.. code-block:: xml

	<property name="factories">
		...
		<entry>
			<key>
				<value>image/png,image/jpeg,image/gif,image/x-bmp</value>
			</key>
			<ref bean="imageFactory" />
		</entry>	
		
For the video mime types the factory concerned is the *videoConversionFactory*, where you can add each mime types desired. 