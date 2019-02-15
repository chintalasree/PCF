1. Using System buildpack
cf app articulate

2. Using Custom buildpack (Java buildpack source)
cf push articulate -p ./articulate-0.2.jar -b https://github.com/cloudfoundry/java-buildpack.git

Note :
-------

We used the Java Buildpack source on Github as our custom buildpack. 
The Java Buildpack source is continuously updated and it is an online package of the 
buildpack. Meaning it has access to all ependencies via the network (it has access to all 
JRE versions, etc). Whereas, the system provided Java buidpack is offline, with a 
limited set of dependencies

