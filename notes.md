
---------------------------------------------------------------------------------------------------------
JENKINS BASICS: 
---------------------------------------------------------------------------------------------------------

JENKINS JOB/ITEM: 

    It is any runnable tasks that is controlled by jenkins. 

    Free Style Project: 
        It is most common type of project. 
        Build type is generally shell for Linux and bash for windows. 
    
    Pipeline: 
        It also called workflow. 
        It is normally written in DSL. 
    
    Multi Configuration: 
        Like free style but more flexibility on environment and configurations. 

---------------------------------------------------------------------------------------------------------

FIRST FREE STYLE PROJECT: 


    New Item (or) Create a job -> Name -> OK 

    Build -> Add build step -> Execute Shell 

---------------------------------------------------------------------------------------------------------

JOB CONFIGURATIONS: 


    General:  General settings. 

        Discard old builds: 
                It helps to remove old builds by using no of builds or no of days to keep.
        GitHub Project:
                To give github project URL. 
        This build requires lockable resources: 
        This project is parametrized: 
                To pass the parameters to the job. 
        Throttle Builds: 
                NO of instance of this job to execute at a time. 
        Disable this project: 
                User wont able to execute the build. 
        Execute concurrent builds if necessary: 


    Source Code Management:  Source code

        Git: 
            Configure the git for the source code. 


    Build Triggers:  On what event this build will be trigered. 

        Trigger build remotely: 
                Use webhook to trigger this build.

        Build after other projects are built:
                Based on another project to trigger this build. 

        Build periodically:
                Based on scheduled timing to trigger the build. 

        Github hook trigger for GIT scm polling: 
                When Jenkins receives a GitHub push hook, GitHub Plugin checks to see whether the hook came from a GitHub repository which matches the Git repository defined in SCM/Git section of this job. If they match and this option is enabled, GitHub Plugin triggers a one-time polling on GITScm. When GITScm polls GitHub, it finds that there is a change and initiates a build. The last sentence describes the behavior of Git plugin, thus the polling and initiating the build is not a part of GitHub plugin.


        Poll SCM:
                Jenkisn poll the SCM to check for any changes frequently and trigger the build.
                This is expensive as multiple calls to git frequently. 


    Build Environment: 

        Delete workspace before build starts: 
                Delete if any earlier executed workspace before start build. 

        Use secret texts or files: 

        Abort the build if its stucks: 
        Add the timestamp to console output:
        Inspect build log for published Gradle build scans:
        With Ant: 


    Build: 

        Execute windows batch command 
        Execute shell 
        Invoke Ant 
        Invoke Gradle Script 
        Invoke Top level maven targets 
        Run with timeout 
        Set build status to pending on github commit 


    Post Build Actions 
        Aggregate downstream test results 
        Archive the artifacts 
        Build other projects 
        Publish junit test result report
        Record fingerprint of files to track changes.
        Git publisher
        Email notification
        Editable email notification
        Set github commit status 
        Set build status on github commit (deprecated)
        Delete workspace when build is done.


---------------------------------------------------------------------------------------------------------

EXECUTE SCRIPTS FROM JENKINS:


    1. Create the sample executable script file (test-script.sh)
    2. Script can be copied by,
            1. Copy to local or container path and use that path in script. 
            2. Commit in git hub and use the $WORKSPACE/test-script.sh 
    3. Use that path to execute the script.


---------------------------------------------------------------------------------------------------------

ADD PARAMETERS IN JENKINS JOB: 

    It helps to pass the parameter dynamically to the jenkins. 

    Select option "This Option is parametrized" -> Choose the paramter format. 
                Select Name, Default value & Description. 
    
    After this "Build" option changed to "Build with parameters".

---------------------------------------------------------------------------------------------------------

LOGICAL INPUT IN JENKINS JOB:

        Here tried to use different parameter types like boolean, choice etc. 


---------------------------------------------------------------------------------------------------------
CONTINUOS INTEGRATION WITH JENKINS: 
---------------------------------------------------------------------------------------------------------

JENKINS INTEGRATION WITH GIT AND GITHUB: 

        1. Manage Jenkins -> Choose the "Git Hub" and "GitHub Integration Plugin".
        

CONFIGURE JAVA & MAVEN IN JENKINS: 

        1. Manage Jenkins -> Global Tool Configuration. 
        2. Enter the JAVA_HOME & MAVEN_HOME path details. 
        3. JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/bin/java  (readlink -f $(which java))
        4. MAVEN=/usr/share/maven


CREATE FIRST MAVEN JOB: 

        1. Dashboard -> New Item -> Free style project -> Name 
        2. Repository used = https://github.com/anshulc55/Jenkins_Upgradev3.git . If puplic repository, then no need of credentials. 
        3. Build -> Invoke Top Level Maven Targets -> Select Advanced -> POM file PATH


SOURCE CODE POLLING IN JENKINS: 

        Build Trigger -> Poll SCM 
                Based on schedule, it polls git hub to look for changes. 
                In Schedule, gives in CRON format.
                IF any changes, then only build will be triggered. 


REMOTE BUILD TRIGGER IN JENKINS:

        Remote build trigger is helpful when to trigger externally. 
        For example some event happening in server A and jenkins running in server B. Based on event in server A, will trigger the jenkin build in server B. 
        Can call the build trigger by some sript, API or UI click.

        Build Trigger -> Trigger builds remotely. 
                1. Enter the authentication token (any value).
                2. Use the below URL to trigger the build, 
                        JENKINS_URL/job/remote-build-trigger/build?token=TOKEN_NAME or buildWithParameters?token=TOKEN_NAME
                3. After click the URL http://localhost:8080/job/remote-build-trigger/build?token=TEST-TOKEN , triggered the job.
        

        Build Trigger -> Build Periodically: 
                Based on the cron schedule, trigget the build periodically. 


DEPLOY THE JAR LOCALLY: 

        1. Use the shell script to execute,
                java -jar jar/file/path.jar 
        2. $WORKSPACE - gives workspace of jenkins. 

        NOTE: If any SPACES with job name, then shell path will be failed. 


PUBLISH TEST RESULTS IN JOB: 

        1. First to get the report path. 
                Surefire report directory: /var/lib/jenkins/workspace/first maven project/maven-samples/single-module/target/surefire-reports
        2. Project -> Configure -> Post Buil Actions -> Publish JUnit test result report.
        3. Enter the path with path/to/*.xml
        3. "Test Result Trend" graph will be shown in job page. 


ARCHIVE LAST SUCCESSFUL ARTIFACT: 

        1. Post Build Actions -> Archive the artifacts.
        2. Files to archive -> Give the file path (maven-samples/single-module/target/single-module-project.jar)
        3. "Last successful artifacts" will be shown in job page. 


---------------------------------------------------------------------------------------------------------
CONTINUOS DELIVERY WITH JENKINS: 
---------------------------------------------------------------------------------------------------------

BUILD PIPELINE PLUGIN: 

        Plugin - Copy Artifacts - Used to copy from one project to another. 
        Plugin - Deploy to Container - Used to deploy to container. 

        1. Created the 2 jobs, 1 to create artifacts. 
        2. 2nd job to copy artifacts and deploy to container. 

BUILD PIPELINE DESIGN: 

        Plugin "build pipeline view" - helps to view the upstream and downstream job.
        "Upstream Projects" & "Downstream Projects" will be shown in job page.

DEPLOY TO PRODUCTION: 

        1. Create the job 1 (with source code)
        2. Create job 2 with Build Triggers -> Build after other projects are built. 
        3. Create job 3.
        4. In job 2, Post build actions -> Build other project (auto) / Build other project (manual)
        
---------------------------------------------------------------------------------------------------------
INFRASTRUCTURE AS CODE: 
---------------------------------------------------------------------------------------------------------






