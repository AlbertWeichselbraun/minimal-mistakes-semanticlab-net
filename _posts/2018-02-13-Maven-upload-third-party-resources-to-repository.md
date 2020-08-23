--- 
title: Deploying third-party artifacts to a local repository with WebDAV
layout: single
categories: ["maven", "java"]
--- 

This guide outlines how to deploy third party jars to a local repository over WebDAV. Using WebDAV requires 
(i) setting up the login data of the WebDAV repository and
(ii) providing a **current** Webdav wagon extension to maven.

1. Configure the Webdav repository in `~/.m2/settings.xml`.
   ```xml
   <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                             http://maven.apache.org/xsd/settings-1.0.0.xsd">
   
   
       <servers>
          <server>
              <id>mywebdavserver</id>
              <username>user</username>
              <password>***</password>
          </server>
       </servers>
    </settings>
    ```

2. Create a *dummy* pom file which provides maven with information on the required Webdav wagon:
   ```xml
   <project>
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.example</groupId>
      <artifactId>webdav-deploy</artifactId>
      <packaging>pom</packaging>
      <version>1</version>
      <name>Webdav Deploy</name>
   
      <build>
         <extensions>
            <extension>
               <groupId>org.apache.maven.wagon</groupId>
               <artifactId>wagon-webdav-jackrabbit</artifactId>
               <version>3.0.0</version>
            </extension>
         </extensions>
      </build>
   </project>
   ```

3. upload the artifact to the repository with `mvn`:
   ```bash
   mvn deploy:deploy-file -Dfile=<path-to-file> \
           -DgroupId=<group-id> \
           -DartifactId=<artificat-id> \
           -Dversion=<version> \
           -Dpackaging=<packaging> \
           -DrepositoryId=mywebdavserver \
           -Durl=dav:<url-to-the-webdav-server>
   ```

   **Example:** deploy the latest libsvm version to our local repository.

   ```bash
   mvn deploy:deploy-file\
       -Dfile=libsvm.jar \
       -DgroupId=tw.edu.ntu.csie \
       -DartifactId=libsvm \
       -Dversion=3.22 \
       -Dpackaging=jar \
       -DrepositoryId=semanticlab.net 
       -Durl=dav:http://semanticlab.net/deploy/
   ```
   

### Literature

* [Guide to deploying 3rd party JARs to remote repository](https://maven.apache.org/guides/mini/guide-3rd-party-jars-remote.html)
* [Deploying jars to third party maven repository via WebDAV](https://www.chrissearle.org/2008/02/10/Deploying_jars_to_third_party_maven_repository_via_WebDAV/)

