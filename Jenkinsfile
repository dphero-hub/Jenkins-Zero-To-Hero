pipeline {
    agent any
    tools {
  maven 'maven'
  jdk 'openjdk11'
}

// parameters {
// 	     string(name: 'BRANCH', defaultValue: 'build-jenkinsfile', description: 'Branch to build')
//     }


    stages {  
        stage('Build the application') {
            dir(java-maven-sonar-argocd-helm-k8s/spring-boot-app){
                steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        }
        stage('Build the application') {
            dir(java-maven-sonar-argocd-helm-k8s/spring-boot-app) {
                steps {
                sh 'java -jar target/spring-boot-app.jar --server.port=8888'
            }
        } 
        }       
        
    }
}