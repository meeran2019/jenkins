pipeline {
  agent any
  environment {
  region = "dev"
  type = "t2-micro"
}
  stages {
    stage('jenkinsfile') {
      steps {
        sh 'echo $WORKSPACE'
      }
    }

    stage('build') {
      steps {
        sh '''cd my-app
mvn clean compile'''
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
  post {
  success {
    echo 'post success'
  }
  failure {
    echo 'post failure'
    }
  }

}
