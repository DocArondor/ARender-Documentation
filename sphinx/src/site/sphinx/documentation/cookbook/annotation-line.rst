Créer une annotation personnalisée par l'exemple : l'annotation ligne
======================================================================

-----------------
L'annotation Line
-----------------
L'annotation Line est tirée de l'annotation Arrow avec les éléments de la tête (head) et de la queue (tail) à None. C'est donc une personnalisation de cette annotation.
Nous avons besoin que de deux fichiers, `arender-custom-integration.xml` et `arender.properties`.

------------------------------------------------
Modification de `arender-custom-integration.xml`
------------------------------------------------
A l'intérieur de ce fichier nous allons faire deux choses. Créer le modèle de l'annotation et faire le bouton qui appelera cette annotation. 

Modèle de l'annotation
----------------------


Pour le faire, on peut partir de la base de l'annotation arrow et la personnaliser. On peut récupérer le bean de arrowCreationAction qui se trouve dans `event-configuration.xml`.
Une fois fait, pour avoir une ligne il faut que la propriété head et la propriété tail soient à NONE.  


Exemple :

.. code-block:: xml

    <bean id="lineCreationAction" class="com.arondor.viewer.client.toppanel.behavior.annotation.CreateAnnotationButtonHandler">
      <constructor-arg>
        <bean class="com.arondor.viewer.client.annotation.events.PrepareAnnotationCreationEvent">
          <constructor-arg>
            <value type="com.arondor.viewer.annotation.common.AnnotationType">Line</value>
          </constructor-arg>
          <property name="model">
            <!-- Annotation class -->
            <bean class="com.arondor.viewer.annotation.api.LineElemType">
              <!-- annotation properties -->
              <property name="head">
                <value type="com.arondor.viewer.annotation.api.LineEndType">NONE</value>
              </property>
              <property name="tail">
                <value type="com.arondor.viewer.annotation.api.LineEndType">NONE</value>
              </property>
            </bean>
          </property>
        </bean>
      </constructor-arg>
    </bean>

..

Il est possible de personnaliser ensuite l'annotation pour avoir une couleur ou une taille par défaut.

Bouton de l'annotation
----------------------
On peut maintenant faire le bouton de l'annotation. On peut partir du modèle de base de la flèche qui se trouve dans `toppannel-annotations-configuration.xml` et le personnalisé.

Exemple :

.. code-block:: xml

    <bean id="addLineAnnotationButton"
		class="com.arondor.viewer.client.toppanel.presenter.ButtonPresenter"
		scope="prototype">
		<property name="enabled" value="${topPanel.annotationMenu.line}" />
		<property name="imageResource"> 
			<bean class="com.arondor.viewer.client.defferedmodules.ExternalImageResource"> 
				<property name="width" value="32" /> <property name="height" value="32" /> 
				<property name="url" value="icons/line.png" />
			</bean> 
		</property> 
		<property name="buttonTitle">
			<value>Line</value> 
		</property>  
		<property name="buttonHandler">
			<ref bean="lineCreationAction" />
		</property>
	</bean>


..

Dans l'exemple l'image est chargé à partir du dossier icons de l'HMI. La value peut aussi être une URL externe provenant d'un site.
 
------------------------------------
Modification de `arender.properties`
------------------------------------

Ajout du bouton
---------------

Si la valeur `topPanel.annotation.buttons.beanNames` n'existe pas rajouter là, et rajouter votre bouton.

Exemple :
`topPanel.annotation.buttons.beanNames=addLineAnnotationButton`

Attention, si vous voulez avoir tout les boutons d'annotations, il faut récupérer le `topPanel.annotation.buttons.beanNames` de `arender-default.properties`et rajouter votre bouton.
Ensuite, il suffit d'activer votre annotation.
Exemple :
`topPanel.annotationMenu.line=true`

Relancer votre HMI et votre annotation line apparaitra. 
