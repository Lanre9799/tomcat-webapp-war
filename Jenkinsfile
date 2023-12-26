node{
  def mvnHome = tool name: "maven3"
  properties([pipelineTriggers([pollSCM('* * * * *')])])
  stage('1. clone code'){
    echo "cloning source code"
    checkout scmGit(branches: [[name: '*/script']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Lanre9799/tomcat-webapp-war.git']])
  }
  stage('2. maven build'){
    echo "building code now"
    sh "${mvnHome}/bin/mvn clean package"
  }
  stage('3. sonarqube'){
    echo "code quality scan"
    sh "${mvnHome}/bin/mvn sonar:sonar"
  }
  stage('4. Nexus'){
    echo "Nexus Artifactory"
    sh "${mvnHome}/bin/mvn deploy"
  }
}
