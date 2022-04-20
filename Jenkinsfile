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

    stage('JUnit Test') {
      steps {
        junit '*'
      }
    }

  }
}