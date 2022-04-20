pipeline {
  agent any
  stages {
    stage('Buzz Build') {
      parallel {
        stage('Buzz Build') {
          steps {
            sh 'echo $WORKSPACE'
          }
        }

        stage('parallel stage 1') {
          steps {
            echo 'parallel stage 1'
          }
        }

        stage('parallel stage 3') {
          steps {
            echo 'parallel stage 3'
          }
        }

      }
    }

    stage('Bees Test') {
      parallel {
        stage('Bees Test') {
          steps {
            sh 'echo $WORKSPACE'
          }
        }

        stage('parallel stage 2') {
          steps {
            echo 'parallel stage 2'
          }
        }

      }
    }

    stage('Archive Artifacts') {
      steps {
        archiveArtifacts(artifacts: 'Jenkinsfile', allowEmptyArchive: true, fingerprint: true)
      }
    }

    stage('display environment') {
      steps {
        echo '$Region'
        echo '$WORKSPACE'
        sh '''echo $Region
echo $WORKSPACE'''
      }
    }

  }
  environment {
    Region = 'us-east-1'
  }
}