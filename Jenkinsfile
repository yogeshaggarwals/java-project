pipeline {
  agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '4', artifactNumToKeepStr: '2'))
  }

  stages {
    stage('build') {
      steps {
        sh 'ant -f build.xml -v'
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
    }
  }
}
