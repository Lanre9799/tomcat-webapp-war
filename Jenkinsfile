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
        git branch: 'declarative', url: 'https://github.com/Lanre9799/tomcat-webapp-war.git'
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
    stage('5. Deploy'){
      steps{
        sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansible-server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '//home//ansible//webapp.yaml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//home//ansible//jenkins', remoteDirectorySDF: false, removePrefix: 'target', sourceFiles: 'target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
          }
      }
  }
}
