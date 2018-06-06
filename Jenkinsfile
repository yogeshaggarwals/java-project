pipeline {
  agent {
    label 'master'
  }

  options {
    buildDiscarder(logRotator(numToKeepStr: '4', artifactNumToKeepStr: '2'))
  }

  stages {
    stage('Unit Tests') {
      steps {    
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
      }
  }

    stage('build') {
      steps {
        sh 'ant -f build.xml -v'
      }
    }

    stage('deploy') {
      steps {
        sh "cp dist/rectangle_${env.Build_number}.jar /var/www/html/rectangles/all/"
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
    }
  }
}
