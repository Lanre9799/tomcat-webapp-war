pipeline{
  agent any
  tools{
    maven 'maven3'
  }
  triggers{
    pollSCM('* * * * *')
  }
  stages{
    stage('1. Git'){
      steps{
        git branch: 'Declarative', url: 'https://github.com/Lanre9799/tomcat-webapp-war.git'
      }
    }
    stage('2. maven'){
      steps{
        sh 'mvn clean package'
      }
    }
    stage('3. sonarqube'){
      steps{
        sh 'mvn sonar:sonar'
      }
    }
    stage('4. Nexus'){
      steps{
        sh 'mvn deploy'
      }
    }
  }
}
