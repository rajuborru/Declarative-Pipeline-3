pipeline {

  agent any
  
  tools {
      maven 'maven'
  }      

     stage('Checkout') {
          steps {
              git 'https://github.com/AugustoPeralta/spring-boot.git'
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
}
