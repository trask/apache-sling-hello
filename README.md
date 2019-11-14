## Setup

1. Download Sling Starter Standalone from https://sling.apache.org/downloads.cgi

2. Download applicationinsights-agent-{version}.jar from https://github.com/microsoft/ApplicationInsights-Java/releases

3. Create file `AI-Agent.xml` with the following content:

   ```
   <?xml version="1.0" encoding="utf-8"?>
   <ApplicationInsightsAgent>
     <Instrumentation>
       <BuiltIn enabled="true">
       </BuiltIn>
     </Instrumentation>
   </ApplicationInsightsAgent>
   ```

4. Put all three files in the same directory

   * org.apache.sling.starter-11.jar
   * applicationinsights-agent-{version}.jar
   * AI-Agent.xml

5. Run sling

    ```
    java -javaagent:applicationinsights-agent-{version}.jar -jar org.apache.sling.starter-11.jar
    ```

## Build sample app

1. Update the instrumentation key in `src/main/resources/ApplicationInsights.xml`

2. Optionally enable debug logging in the `ApplicationInsights.xml` file by uncommenting 

   ```
   <SDKLogger type="CONSOLE">
     <Level>TRACE</Level>
   </SDKLogger>
   ```

   and

   ```
   <Channel>
     <DeveloperMode>true</DeveloperMode>
   </Channel>
   ```

2. Build with maven

   ```
   mvn clean package
   ```

## Deploy the bundle to Sling

1. Go to `http://localhost:8080/system/console/bundles`

2. Log in with `admin`/`admin`

3. Click `Install/Update...`

4. Select the bundle from `target/apache-sling-sample-1.0-SNAPSHOT.jar`

5. Check `Start Bundle`

6. Click `Install or Update`

## Test the app

1. Go to `http://localhost:8080/hello-world-servlet`

2. Request and dependency telemetry should show up in Azure Portal within a couple of minutes

3. If you turned on debug logging above, you should see the captured request and dependency telemetry json in the console window right away (where you ran `java -javaagent:... -jar ...`)
