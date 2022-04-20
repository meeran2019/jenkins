pipeline {
  agent any
  stages {
    stage('Buzz Build') {
      steps {
        sh './jenkins/build.sh'
      }
    }

    stage('Bees Bees') {
      steps {
        sh './jenkins/test-all.sh'
      }
    }

  }
}