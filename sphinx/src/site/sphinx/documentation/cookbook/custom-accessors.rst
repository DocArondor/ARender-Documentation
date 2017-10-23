Créez votre propre connecteur de documents
==========================================


En fonction du type de service que vous souhaitez utiliser, nous avons peut-être déjà chez nous un connecteur pour ce type de service. N'hésitez donc pas à venir vers nous en premier lieu.

Si vous préférez directement implémenter votre connecteur, il y aura deux étapes à suivre:


Créer un parseur d'URL, qui va prendre de l'URL d'ARender les paramètres nécessaires et créer ensuite le second composant dont vous aurez besoin : le document accessor.

http://arender.fr/rendition-api/com/arondor/viewer/rendition/api/DocumentServiceURLParser.html


La méthode canParse retourne vrai si les paramètres contenus dans l'URL d'ARender sont suffisants pour pouvoir parser le document.


La méthode parse doit parser les paramètre de l'URL et pousser un DocumentAccessor en rendition, en voici un exemple:

.. code-block:: java

	List<DocumentIdParameter> parameters = new ArrayList<DocumentIdParameter>();
	parameters.add(new URLDocumentIdParameter(URL_REQUEST_PARAMETER, url));
	DocumentId documentId = DocumentIdFactory.getInstance().generate(parameters);
	DocumentAccessor documentAccessor = new DocumentAccessorURL(url, documentId);
	documentService.loadDocumentAccessor(documentAccessor);
	return documentAccessor.getUUID();

Ici, au lieu d'un DocumentAcessorURL, vous mettrez votre propre document accessor.

http://arender.fr/rendition-api/com/arondor/viewer/rendition/api/document/DocumentAccessor.html


Les méthodes détaillées dans la documentation concernant les DocumentAccessor sont très simples et parlent d'elles même et ne devraient pas vous causer de soucis d'implémentation.

Une fois que vous avez développé votre couple Parser/Accessor vous serez capable d'ajouter le Parser au fichier arender.xml contenu dans le dossier WEB-INF/classes du war ARender.

.. code-block:: xml

	<property name="registeredURLParsers">
		<list>
			<bean class="full.class.name.here.YourCustomURLParser" />
			<bean
				class="com.arondor.viewer.server.servlet.urlparser.FallbackURLParser" />
		</list>
	</property>

Dans le scénario de création d'un Accessor/Parser nous vous recommandons fortement de faire un project Maven et d'utiliser un analyseur XSLT afin de modifier le fichier XML automatiquement sans écraser des modifications apportées par les nouvelles versions.
