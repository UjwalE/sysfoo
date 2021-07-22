pipeline {
  agent none
  stages {
    stage('build') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'Compiling using maven'
        sh 'mvn compile';
      }
    }

    stage('test') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
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
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      when {
        branch 'master'
      }
      steps {
        echo 'Generating WAR'
        sh 'mvn package'
      }
    }

    stage('Docker BnP') {
      agent any
      when {
        branch 'master'
      }

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

    stage('Deploy to Dev') {
      when {
             beforeAgent true
             branch  'master'
           }

      agent any

      steps {
        echo 'Deploying to Dev Environment with Docker Compose'
        sh 'docker-compose up -d'
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
