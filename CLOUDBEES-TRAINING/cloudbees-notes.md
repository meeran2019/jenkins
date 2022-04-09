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

    

