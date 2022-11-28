
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
        script{
          // groovy script. 
        }
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
