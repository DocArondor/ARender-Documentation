Ajout de type mime image/vidéo supportés
========================================

Si votre serveur de rendition ne possède pas tous les types mimes que vous souhaitez utiliser, il est possible que le serveur puisse tout de même convertir votre fichier.

Dans le cas d'une conversion image ou vidéo, la liste exhaustive des fichiers images/vidéos supportés par imagemagick/ffmpeg est longue. 

Si vous souhaitez rajouter un type mime, il suffit de modifier le fichier *arender-rendition.xml* du dossier conf/ de votre rendition.

Par exemple, si nous souhaitons ajouter le type mime *image/x-bmp* : 

.. code-block:: xml

	<property name="factories">
		...
		<entry>
			<key>
				<value>image/png,image/jpeg,image/gif</value>
			</key>
			<ref bean="imageFactory" />
		</entry>	
		
Deviendrait alors: 

.. code-block:: xml

	<property name="factories">
		...
		<entry>
			<key>
				<value>image/png,image/jpeg,image/gif,image/x-bmp</value>
			</key>
			<ref bean="imageFactory" />
		</entry>	

Pour les types mime, la factory concernée est la *videoConversionFactory*, où vous pouvez ajouter chaque type mime désiré. 