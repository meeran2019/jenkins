pipeline {
  agent any
  stages {
    stage('Buzz Build') {
      steps {
        sh 'echo $WORKSPACE'
      }
    }

    stage('Bees Test') {
      steps {
        sh 'echo $WORKSPACE'
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