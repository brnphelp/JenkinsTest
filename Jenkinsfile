pipeline{
  agent{
    docker{
      image 'node:6-alpine'
      args '-p 3000:3000'
    }
  }
  environment{
    CI = 'true'
  }
  stages {
    stage('build'){
      steps{
        sh 'npm install'
      }
    }
    stage('test'){
      steps{
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('Deliver'){
      steps{
        sh './jenkins/scripts/deliver.sh'
      }
    }
    stage('SonarQube analysis') {
      steps{
        withSonarQubeEnv('My SonarQube Server') {
          sh 'mvn clean package sonar:sonar'
          } // SonarQube taskId is automatically attached to the pipeline context
      }
    }

  }
}
