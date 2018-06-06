pipeline {
  agent none

  options {
    buildDiscarder(logRotator(numToKeepStr: '4', artifactNumToKeepStr: '2'))
  }

  stages {
    stage('Unit Tests') {
    agent {
      label 'cent'
    }
      steps {    
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
      }
  }

    stage('build') {
    agent {
      label 'cent'
    }
      steps {
        sh 'ant -f build.xml -v'
      }
      post {
        success {
          archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
        }
      }

    }

    stage('deploy') {
    agent {
      label 'cent'
    }
      steps {
        sh "cp dist/rectangle_*${env.Build_number}.jar /var/www/html/rectangles/all/"
      }
    }
  }
}
