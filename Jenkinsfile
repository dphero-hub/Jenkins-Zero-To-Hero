pipeline {
    agent {
        label 'built-in'
    }
    tools {
  maven 'maven'
  jdk 'openjdk17'
}

// parameters {
// 	     string(name: 'BRANCH', defaultValue: 'build-jenkinsfile', description: 'Branch to build')
//     }


    stages {  
        stage('Build the application') {
           
                steps {
                    dir('java-maven-sonar-argocd-helm-k8s/spring-boot-app') {
                        sh 'mvn clean package -DskipTests'
                    }


        }
        }
        stage('start the application') {
            
                steps {
                    dir('java-maven-sonar-argocd-helm-k8s/spring-boot-app') {
                        sh 'nohup java -jar target/spring-boot-web.jar --server.port=8888 > /dev/null 2>&1 &'
                }
        } 
        }       
        stage('test the application') {
            
                steps {
                    sh 'curl localhost:8888'
        } 
        }            
    }
}