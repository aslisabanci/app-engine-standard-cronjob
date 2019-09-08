Cron Job for App Engine - Standard Environment Java 8 App
============================

## Current config
- Apache Maven 3.6.2 (40f52333136460af0dc0d7232c0dc0bcf0d9e117; 2019-08-27T17:06:16+02:00)
- Java version: 1.8.0_221

## Deploy App with Maven
Run the command `mvn appengine:deploy` in the folder where `pom.xml` sits under.

## Cron Job Setup
### cron.xml

`cron.xml` file should be under the `WEB-INF` folder, next to `appengine-web.xml` file. 

What it looks like:
```
<?xml version="1.0" encoding="UTF-8"?>
<cronentries>
    <cron>
        <url>/hello</url>
        <description>test cron</description>
        <schedule>every 6 hours</schedule>
    </cron>
</cronentries>
```

### pom.xml
Important section of the `pom.xml` to correctly tell our Maven to build and deploy this is: 

```
  <build>
    <outputDirectory>${project.build.directory}/${project.build.finalName}/WEB-INF/classes</outputDirectory>
    <plugins>
      <plugin>
        <groupId>com.google.appengine</groupId>
        <artifactId>appengine-maven-plugin</artifactId>
        <version>1.9.63</version>
        <configuration>
          <appId>makine-degil-yapay</appId>
          <version>2</version>
        </configuration>
      </plugin>
    </plugins>
  </build>
```

## Update Cron Job
Run the command `mvn appengine:cron_update` again in the folder of the `pom.xml` file to get the cron job configured. 

When the command runs successfully, expect to see your cron job listed under the Cron Jobs section of your App Engine dashboard.



