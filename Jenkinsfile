pipeline {
  agent any
  tools{
      maven 'Maven 3.8.1'
  }
  stages{
      stage('build'){
          steps{
              echo 'Compiling using maven for branch test'
              sh 'mvn compile'
          }
      }
      stage('package'){
          steps{
              echo 'Generating WAR'
              sh 'mvn package'
          }
      }
  }

  post{
    always{
        echo 'This pipeline is completed..'
    }
  }
}
