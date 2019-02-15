Deploy into Tomcat
----------------------

cf push myapp -p simple.war --random-route


Deploy into JBoss
--------------------

cf push myapp -p simple.war --random-route -b https://github.com/cloudfoundry-community/jboss-buildpack