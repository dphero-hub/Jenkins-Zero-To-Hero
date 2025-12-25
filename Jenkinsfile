pipeline {
    agent {
        label 'built-in'
    }
    tools {
  maven 'maven'
  jdk 'openjdk11'
}

// parameters {
// 	     string(name: 'BRANCH', defaultValue: 'build-jenkinsfile', description: 'Branch to build')
//     }


    stages {  
        stage('Build the application') {
           
                steps {
                 dir(java-maven-sonar-argocd-helm-k8s/spring-boot-app){
                   sh 'mvn clean package -DskipTests'
            }
        }
        }
        stage('test the application') {
            
                steps {
                    dir(java-maven-sonar-argocd-helm-k8s/spring-boot-app) {
                sh 'java -jar target/spring-boot-app.jar --server.port=8888'
            }
        } 
        }       
        
    }
}