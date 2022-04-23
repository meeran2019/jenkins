---------------------------------------------------------------------------------------------------------
JENKINS ESSENTIAL
---------------------------------------------------------------------------------------------------------

    Discussed about CI, CD, git and test details. 

---------------------------------------------------------------------------------------------------------
JENKINS ADMINISTRATION:
---------------------------------------------------------------------------------------------------------

    $JENKINS_HOME = /var/lib/jenkins  (default jenkins file path)


JENKINS UPGRADE: 

    https://university.cloudbees.com/jenkins-administration-1-essentials/769786

    1. On Linux, replace jenkins.war file to /usr/share/jenkins


MANAGE JENKINS: 

    Jenkins Controller      -   Master which control all. 
    Jenkins Node (Can be Linux server, Windows server etc)      -   Execute the tasks.
    Executor -  a thread for execution of tasks. no of concurrent tasks executed at a time.
    agent   -   tool manages the executors on remote node. 


SYSTEM CONFIGURATION: 

    CONFIGURE SYSTEM: 

        Configure many standard aspects of jenkins including JDK installation, Build tools installation, Version control tools etc.
        Configure global systems and path. 

    GLOBAL TOOLS CONFIGURATION: 

        To configure tools used for pipeline.
        Depends upon plugin, additional configuration added. 
        Configure many standard aspects of jenkins including JDK installation, Build tools installation, Version control tools etc.
        Multiple version of maven or jdk can be installed. 

---------------------------------------------------------------------------------------------------------

MANAGE PLUGINS: 

    Many features are implemented with multiple plugins and many plugins have dependencies on other plugins.

    Plugin is a jar file and stored under $JENKINS_HOME/plugins directory. 

    Manage Jenkins -> System Information - To see a list of plugins. 

    Enabled/Disabled plugins - NOTE: To enable/disable plugins. Suggest to go for disable instead of uninstall.

    Plugins can also install manually without using UI.


BUILD NOTIFICATIONS: 

    Jenkins allow to send notifications through email, slack or other channels. 

    Manage Jenkins -> Configure System

    Some plugins used are ,
        cleaning up and notifications, Notification plugin, email-ext plugin, mailer plugin, slack plugin.

---------------------------------------------------------------------------------------------------------

WORKING WITH NODES: 

    Node is a server where jenkins run build jobs. Agent is a tool that manages build execution on the node. 
    Available nodes and agent listed on "Build executor status".

    Manage Jenkins -> Manage Nodes and Clouds. 


BUILD AGENTS: 

    Manage Jenkins -> Configure Global Security -> enable "TCP Port for JNLP agents" to random.

    https://bhargavamin.com/how-to-do/setup-jenkins-slave-amazon-linux-aws/

    https://university.cloudbees.com/jenkins-administration-1-essentials/868943



---------------------------------------------------------------------------------------------------------
SECURITY: 
---------------------------------------------------------------------------------------------------------

    To select authentication method - Manage Jenkins -> Configure Global Security -> Security Realm 

    To manage users - Manage Jenkins -> Security -> Manage users.

    To select authorization - Manage Jenkins -> Configure global security -> Authorization

    Accounting: 
        Auditing can be done by using "Audit Trail Plugin".

    Global Security Settings: 

        Port for inbound agents: 
            It can be used to launch an application on client desktop by using resources that are hosted on remote server. 

        Configure credential provider: 
            It allow to choose provider like git hub, artifactory etc. 

        Manage Credentials: 
            Used to store the credentials in different format. 


FOLDERS: 

    It can be created with separate namespace for different projects with same name and helps to simplify the pipeline. 

    Move - Helps to move job from one folder to another.

    (Move button can seen left side of pipeline)


MONITOR JENKINS: 

    Manage Jenkins -> Status Information
        
        System log - To display system logs. 

        Load Statistics - To track utilization of executors. 


RUNNING BACKUPS: 

    $JENKINS_HOME directory to be backedup.
    ./confix.xml file 

    https://university.cloudbees.com/jenkins-administration-1-essentials/769813


---------------------------------------------------------------------------------------------------------

AUTOMATE JENKINS:    

    jenkins CLI can be used.

    Manage Jenkins -> Tools and Actions -> Jenkins CLI 

    1. Download the jenkins-cli.jar file
    2. Run the command  "java -jar jenkins-cli.jar -s http://localhost:8080/ -webSocket help "
            -s - URL to connecto to jenkins.
    3. Manage Jenkins -> Tools and Actions -> Jenkins CLI -> Available commands -> Gives list of core jenkins available command. 
        By using plugins, can contribute additional commands. 

    JENKINS SCRIPT: 

        Can also use groovysh/groovy in CLI. 
                "java -jar jenkins-cli.jar -s http://localhost:8080/ groovysh "

    JENKINS API: 

        curl -X POST \
        --data token=${TOKEN} \
        --data-urlencode json=`{"parameter": [{"name":"id", "value":"123"}, \
            {"name":"verbosity"}, "value":"high"}]}` \
        http://${JENKINS_URL}/job/${MY_PROJECT}/build/api


    SCRIPT CONSOLE: 

        It helps to type in and execute an arbitrary groovy script on the server. 
            Manage Jenkins -> Tools and Actions -> Script Console.


    RELOAD CONFIGURATION FROM DISK: 

        If any configuration changes through CLI, it will require ro refresh to update the configuration.

        Manage Jenkins -> Tools and Actions -> Reload configuration from disk.

    
---------------------------------------------------------------------------------------------------------
PIPELINE AS CODE: 
---------------------------------------------------------------------------------------------------------

    Pipeline is defined in jenkinsfile that uses DSL based on groovy script. 
    Deployment flow is expressed as Code.
    jenkinsfile can be stored in SCM.


PIPELINE SECTION: 

    jenkinsfile that defines the pipeline uses DSL(Domain Specific Language) based on Apache Groovy.

    It consists of following structure, 

        pipeline 
            agent   -   It defines the node where the programs and script to be executed. 
                Stages  -   It defines the work to be done. 
                    Steps   -   Execute the actual program and scripts to be run. 


    DECLARATIVE vs SCRIPTED PIPELINE: 

        Scripted: 
            Uses Pipeline DSL Groovy to define build steps and accomplish in single script that would require many freestyle jobs chained together.
            Executed serially from top to bottom.
            Relies on groovy expression.

        Declarative: 
            It helps to define a pipeline without learn groovy.
            It offers predefined structure. 

        http://localhost:8080/job/test-pipeline-project/directive-generator/

        Snippet Generator                   -   Used to generate the script. 
        Declarative Directive Generator     -   Used to generate the pipeline code for declarative. 

    BLUE OCEAN GRAPHICAL EDITOR: 

        It simplies the tasks of create and running declarative pipelines.
        It integrate with Git, github etc. 


SKELETAL PIPELINE USING BLUE OCEAN: 
    
    https://university.cloudbees.com/jenkins-pipeline-1-essentials/756201

    1. Jenkins -> Open Blue Ocean 
    2. Blue Ocean -> Create Pipeline -> Select Source (Git, Github etc).
        click ctrl + S to update jenkins file manually.
    
        pipeline {
            agent any
            stages {
                stage('Buzz Buzz') {
                steps {
                    echo 'Bees Buzz!'
                }
                }

                stage('Bees Bees') {
                steps {
                    echo 'Buzz, Bees, Buzz!'
                    echo 'Bees Buzzing!'
                    echo 'Bees Buzzing Again'
                }
                }

            }
            }

    WORKING ON FEATURE BRANCH: 

        1. Jenkins -> Blue Ocean -> New Pipeline 
        2. Select Github -> Select repository -> create pipeline.
        3. Click Modify -> Click Save -> Save to new branch
    
ARTIFACTS AND FINGERPRINTS: 

    Artifact is file produced as a result of jenkins build. 
    By default, stored on jenkins master not on the agent.
    If not archived, they deleted when pipeline completes and workspace is wiped.
    Archive the files in ${JENKINS_HOME}.

    Fingerprint is md5 checksum of artifact.
    Each archived artifact can be fingerprinted.

    ARTIFACTS PATTERN: 
        my-app.zip  -   file at workspace root.
        images/*.png    -   .png files under image folder under workspace root.
        target/**/*.jar -   all jar files recursively under target folder under workspace root.

        "Copy Artifact Plugin" is used to copy artifacts from one project to another project. 

        Artifact is coupled with build retention policy. Deleting build will delete the artifacts. 


ADDING JUNIT STEP: 

    JUnit is testing framework for java programs.
    JUnit plugin provide steps that implement JUnit as publisher which consumes XML test reports and generates some graphical visualisation of test results.

    Add Steps -> Archive JUnit-formatted test results -> .xml file should be maintained.


ENVIRONMENT VARIABLES: 

    System defined environment variables can be taken from Manage Jenkins -> System Information.

    In Blue Ocean -> Start -> Environment -> Enter the Key & Value pair.

    In Shell script step, use with $KEY1


DEFINE PARALLEL STAGES: 

    By default, if one parallel stage fails, other stages continue to execute it.
        Add "failfast true" to force all parallel stage to abort if one stage fails.
    
    Use few parallel stages and avoid multiple parallel stages.

    
MULTI-BRANCH PIPELINE IN OLD-UI: 
    
    https://university.cloudbees.com/jenkins-pipeline-1-essentials/791029

    1. Jenkins -> New Item -> Multi branch pipeline 
    2. Select source repo and branch details.
    3. If multiple branches, then all branches are executed separately.


HINTS - PIPELINE STRUCTURE: 

    1. Most of the pipeline is a series of steps that define the tasks to be executed.
    2. Use minimum amount of code to connect pipeline steps and integrate tools.
        Delegate most activity to steps that execute on agents and reduce load on masters.
    3. Use command line tools for operations like,
        Command line client for APIs: 
            Use bash or sh script to integrate.
                sh "java -jar client.jar $endPointUrl $inputData"
    4. Use most used/well maintained Plugins.
    5. Reduce the no of steps in pipeline. 
    6. Log data stored in master. Manage logs helps to reduce load.


BUILD TOOLS TO CREATE CODE FOR STEPS: 

    Virtually any build tool (like Make, Ant, Maven, Gradle, NPM etc) can be used with jenkins.
    For any of these build, can run by using sh for linux and bat for windows.
        ex: sh 'mvn clean install'
            bat 'mvn clean install'
            sh 'npm build'
            bat 'npm build'


    ADDING TOOLS TO PIPELINE: 

        Use tools section to define tools to auto install and put them on $PATH.
        tools section can be applied at both pipeline level or stage level.
        values used to define each tool must be configured on manage jenkins -> Global tool configuration.
        
            Tools supported without additional plugin: 
                maven, jdk, gradle, nodejs
            
            pipeline {
            agent any
            tools {
                maven 'Maven 3.3.9'
                jdk 'jdk8'
            }
        ...
        }

        Common practice is to use maven at pipeline level and jdk at stage level. so pipeline allow to build for multiple jdk versions.


POST section defined at pipeline or stage level. 

        it is based on conditions like always, success, unsuccessful etc.
            post{
                always{
                    echo "post condition"
                }
            }

---------------------------------------------------------------------------------------------------------

PIPELINE SYNTAX: 

    Jenkins Dashboard -> Select Pipeline -> Pipeline Syntax
        It displays Snippet generator & Declarative director generator.
    

AGENT SECTION:

    It can be define at pipeline level or stage level.

    To run all stages in any available agents:
        pipeline {
            agent any
            ....
            }

    To run all stages on specific agents: 
        pipeline {
        agent { label 'bzzzmaven' }
        ....
        }

    To run all stages on container with specific image: 
        pipeline {
        agent { docker 'bzzzcentos:7' }
        ....
        }

    To run at specific stage agent:  Pipeline Agent is None.

       pipeline {
        agent none
        stages {
            stage ('Build') {
            agent { label 'bzzzmaven' }
            steps { ... }
            }
            stage ('Deploy') {
            agent { label 'bzzzproduction' }
            steps { ... }
            }
        }
        }


STASH/UNSTASH STEPS: 

    Stash step is used to save a set of file for later use in same build.
        Files are archived in compressed tar file suitable for < 5 MB.
            In steps, select "Stash some files to be used later in the build".

    Unstash step is used to restore the stashed file into current workspace. 
            In steps, select "Restore files previously stashed"


INTERACTIVE INPUT: 

    Provides ability to pause the pipeline and wait for input from human.
        In Steps, select "Wait for interactive input"

            stage('confirm for deployment') {
            steps {
                input(message: 'Approve or Reject', ok: 'lets do it')
            }
            }


POST SECTION: 

    Post section contains steps to be executed at end of pipeline or stage.
    It is divided into condition like success, failure , always etc.

    NOTE: Post is not supported in blue ocean interactive. It requires to update in Jenkinsfile.


ENVIRONMENT DIRECTIVE:

    It is key value pair. It can be specify at pipeline or stage level. 
    

NOTIFICATIONS: 

    Jenkins can send notification through email, slack to alert when build starts and succeed/failed.
    Need to install corresponding plugin to support notification method.
        Slack Notification Plugin, Email-ext plugin, 

            stage('notification') {
          steps {
            emailext(subject: 'jenkins - build -start', body: 'build started', to: 'sheikmeeran.sj@gmail.com')
          }
        }


        steps {
            // send build started notifications
            slackSend (color: '#FFFF00', message: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
            }


WHEN DIRECTIVE: 

    when directive specifies condition that must be met for the pipeline to execute the stage.

    Condition can be based on branch, environment, expression, equals, changeRequest, buildingTag,
    tag, beforeAgent (when evaluate the when condition), allof (when all nested condition are true), 
    anyof(atleast one of nested condition is true)

    NOTE: If specific stage condition is not satisfied, then that stage wont execute and move to another stage for execution. It will not stop at that stage.


CREDENTIALS: 

    There are 2 types Global and System. 
    System is specific to Jenkins and Nodes.
    Global is apply to all including Jenkins, Nodes, Items etc.

    Use "WithCredentials" , it generated from snippet generator.

        withCredentials([usernameColonPassword(credentialsId: 'github', variable: 'git')]) {
        // some block
        }   


OPTIONS & CONFIGURATIONS: 

    Options are set inside the jenkinsfile in declarative.
    Configuration is set in classic UI.

    NOTE: Scripted Pipelines and Freestyle jobs support the wrap step that builds wrappers or "environment configuration"; Declarative Pipeline does not support wrappers.


PIPELINE PARAMETERS: 

    Parameters provides the list of parameters user should provide when triggering the pipeline.
    During build, parameter value will be asked and default value can be overridden.
    parameters {
    string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: '')
    }    


SHARED LIBRARIES: 

    It is a separate SCM repo that contains reusable functions which can be called from pipeline.
    It is configured once per jenkins instance.


TRIGGERS DIRECTIVE: 

    triggers are used to trigger pipeline in special condition.
    It is rarely used in modern pipelines.
    
    It is useful in, 
        Perform periodic tasks 
        Trigger build remotely using curl and auth token.
        From parent, to trigger chils pipeline.
    
    Supported trigger types are,
        cron
        pollSCM
        upstream

    Triggers are specified at top level of pipeline. 
        pipeline {
        agent any
        triggers {
            cron('H */4 * * 1-5')
        }


---------------------------------------------------------------------------------------------------------

SAMPLE JENKINS FILE: 

pipeline {
  options {
  timeout(time: 30, unit: "SECONDS")
  }
  parameters {
  string defaultValue: 'pipeline', name: 'type-s'
}
  agent any
  stages {
    stage('jenkinsfile') {
      when {
        branch 'master'
      }
      steps {
        sh 'echo $WORKSPACE'
      }
    }

    stage('build') {
      parallel {
        stage('build') {
          steps {
            sh '''cd my-app
mvn clean compile'''
          }
        }

        stage('options') {
          steps {
            sleep 30
          }
        }

      }
    }

    stage('test') {
      parallel {
        stage('test') {
          steps {
            sh '''cd my-app
mvn clean install'''
          }
        }

        stage('stash-stage') {
          steps {
            stash(name: 'stash-file', allowEmpty: true)
          }
        }

      }
    }

    stage('test-archive') {
      steps {
        archiveArtifacts '**/target/*.jar'
      }
    }

    stage('unstash') {
      steps {
        unstash 'stash-file'
      }
    }

    stage('display-ws') {
      steps {
        sh '''echo $WORKSPACE
ls '''
      }
    }

    stage('confirm for deployment') {
      steps {
        input(message: 'Approve or Reject', ok: 'lets do it')
      }
    }

    stage('display value') {
      steps {
        echo 'deployed successfully'
      }
    }

  }
  environment {
    region = 'dev'
    type = 't2-micro'
  }
  post {
    success {
      echo 'post success'
    }

    failure {
      echo 'post failure'
    }

  }
}

---------------------------------------------------------------------------------------------------------