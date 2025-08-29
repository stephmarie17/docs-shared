In your IDE, create a new `Maven <https://maven.apache.org/>`__ or
`Gradle <https://gradle.org/>`__ project. Add the Bill of
Materials (BOM) for MongoDB JVM artifacts to your project to
organize dependency versions. The BOM simplifies dependency
management by ensuring that you maintain consistent and compatible
versions of dependencies, such as between the {+driver-short+} and
the core driver library. Use the BOM to avoid version conflicts
and simplify upgrades.

Select from the following :guilabel:`Maven` and :guilabel:`Gradle` tabs
to view instructions for adding the BOM for each dependency manager:

.. tabs::

   .. tab:: Maven
      :tabid: maven bom
      
      Add the following code to the ``dependencyManagement`` list in your
      ``pom.xml`` file:

      .. code-block:: xml

         <dependencyManagement>
             <dependencies>
                 <dependency>
                     <groupId>org.mongodb</groupId>
                     <artifactId>mongodb-driver-bom</artifactId>
                     <version>{+full-version+}</version>
                     <type>pom</type>
                     <scope>import</scope>
                 </dependency>
             </dependencies>
         </dependencyManagement> 

   .. tab:: Gradle
      :tabid: gradle bom

      Add the following code to dependencies list in your
      |gradle-filename| file:

      .. code-block:: groovy

         dependencies {
             implementation(platform("org.mongodb:mongodb-driver-bom:{+full-version+}"))
         }

To view a list of dependencies that the BOM manages, see
the `mongodb-driver-bom dependency listing
<https://mvnrepository.com/artifact/org.mongodb/mongodb-driver-bom/{+full-version+}>`__
on the Maven Repository website.
