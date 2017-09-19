
Profiles
--------

  ``mvn enforcer:display-info``


To install the Oracle jdbc drivers
----------------------------------

ojdbc6.jar
---------

  ``mvn install:install-file -Dfile={Path/to/your/ojdbc6.jar} -DgroupId=com.oracle -DartifactId=ojdbc6 -Dversion=11.2.0 -Dpackaging=jar``

ojdbc7.jar
----------
  ``mvn install:install-file -Dfile={Path/to/your/ojdbc7.jar} -DgroupId=com.oracle -DartifactId=ojdbc7 -Dversion=12.1.0 -Dpackaging=jar``
