pipeline {

  agent any
  
  tools {
      maven 'maven'
  }
 
  stages {
     stage('Workspace Prep') {
          steps {
              checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '287fcaab-1a9e-4fad-93d2-2d0f5cb3b5b3', url: 'https://github.com/AugustoPeralta/spring-boot.git']]])
          }
     }
    
     stage('Unit Testing') {
          steps {
              sh 'mvn clean package'
          }
     }                
    
     stage('Code Analysis') {
          steps {
             junit allowEmptyResults: true, testResults: '**/target/**/TEST*.xml'
             archive 'target/*.jar'
          }
     }
     stage('Build App Code') {
          steps {
             junit allowEmptyResults: true, testResults: '**/target/**/TEST*.xml'
             archive 'target/*.jar'
          }
     }
     stage('ALA tool Messaging') {
          steps {
             junit allowEmptyResults: true, testResults: '**/target/**/TEST*.xml'
             archive 'target/*.jar'
          }
     }
     stage('Trigger ALM') {
          steps {
             junit allowEmptyResults: true, testResults: '**/target/**/TEST*.xml'
             archive 'target/*.jar'
          }
     }

    stage('Automated Testing') {
          steps {
             withSonarQubeEnv('sonar') {
              // requires SonarQube Scanner for Maven 3.2+
              sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar'
             }             
          }
    }    
  }
}
