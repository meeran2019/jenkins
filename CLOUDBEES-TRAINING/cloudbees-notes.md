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

    Accouting: 
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




    



        

