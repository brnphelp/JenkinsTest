pipeline{
  agent{
    docker{
      image 'node'
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
        withSonarQubeEnv('LocalSonarQube') {
          // requires SonarQube Scanner for Gradle 2.1+
          // It's important to add --info because of SONARJNKNS-281
          sh './gradlew --info sonarqube'
        }
      }
  }

  }
}
