pipeline {
  agent none
  agent {
    label 'cent'
  }

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
    stage("Running on CentOS") {
      agent {
        label 'cent'
      }
      steps {
        sh "wget http://10.67.130.102/rectangles/all/rectangle_*${env.Build_number}.jar"
        "java -jar rectangle_*${env.Build_number}.jar 3 4"
      }
    }
    stage("Test on Deb") {
      agent {
        docker 'openjdk:8u171-jre'
      }
      steps {
        sh "wget http://10.67.130.102/rectangles/all/rectangle_*${env.Build_number}.jar"
        "java -jar rectangle_*${env.Build_number}.jar 3 4"
      }
    }

  }

}
