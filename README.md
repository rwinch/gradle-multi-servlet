This demonstrates how to have two jars that require different versions of the servlet apis. The build is fairly specific to the Spring build, but can probably be adapted to work with other builds. Some important points:

* The projects exist as two different projects so that they can import cleanly into Eclipse. This is necessary because Eclipse cannot have distinct classpaths per project.
* The merge-dist.gradle file will ensure that the contents of the project it is imported on will merge the contents of javadoc, sourcesJar, and jar.
* We cannot merge javadocJar otherwise the index will not contain all the classes
* We also dynamically add the dependencies to our maven pom from the project that is getting merged to the project we are merging into
* The links to the dependent classes may not be correct. This is due to the fact that we cannot link to both Servlet 3 and Servlet 2.5 API's on the same javadoc generation. We cannot split the javadoc generation up otherwise the index file will be incorrect. There may be a potential to do a hybrid approach and merge some of the files, but further investigation would be necessary.

A quick test can be ran by running

<pre>
  gradle build -x reference
</pre>
