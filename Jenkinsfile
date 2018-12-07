pipeline {

  agent any
  
  tools {
      maven 'maven'
  }
 
  stages {
     stage('Checkout') {
          steps {
              checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '287fcaab-1a9e-4fad-93d2-2d0f5cb3b5b3', url: 'https://github.com/AugustoPeralta/spring-boot.git']]])
          }
     }
    
     stage('Build') {
          steps {
              sh 'mvn clean package'
          }
     }                
    
     stage('Archive') {
          steps {
             junit allowEmptyResults: true, testResults: '**/target/**/TEST*.xml'
             archive 'target/*.jar'
          }
     }
    stage('SonarQube analysis') {
          steps {
             withSonarQubeEnv('sonar') {
              // requires SonarQube Scanner for Maven 3.2+
              sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar'
             }             
          }
    }    
  }
}
