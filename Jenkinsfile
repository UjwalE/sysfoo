pipeline {
  agent none
  stages {
    stage('build') {
      agent {
        docker {
          image 'Maven 3.8.1'
        }

      }
      steps {
        echo 'Compiling using maven'
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'Maven 3.8.1'
        }

      }
      steps {
        echo 'Running Unit Test'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      agent {
        docker {
          image 'Maven 3.8.1'
        }

      }
      steps {
        echo 'Generating WAR'
        sh 'mvn package'
      }
    }

    stage('Docker BnP') {
      agent any
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
            def dockerImage = docker.build("ujwale/sysfoo:v${env.BUILD_ID}", "./")
            dockerImage.push()
            dockerImage.push("latest")
            dockerImage.push("dev")
          }
        }

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