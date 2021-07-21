pipeline {
  agent {
    docker {
      image 'maven:3.6.3-jdk-11-slim'
    }

  }
  stages {
    stage('build') {
      steps {
        echo 'Compiling using maven for branch test'
        sh 'mvn compile'
      }
    }

    stage('package') {
      steps {
        echo 'Generating WAR'
        sh 'mvn package'
      }
    }

  }
  tools {
    maven 'Maven 3.8.1'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}