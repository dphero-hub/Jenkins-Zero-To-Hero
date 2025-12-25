pipeline {
  environment{
    sonar_server = "slave.mytechblog.xyz"
    RELEASE_VERSION = "1.0.${BUILD_NUMBER}"
  }
  agent {
    label 'built-in'
    // docker {
    //   image 'abhishekf5/maven-abhishek-docker-agent:v1'
    //   args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
    // }
  }
  stages {
    // stage('Static Code Analysis') {
    //   environment {
    //     SONAR_URL = "http://${sonar_server}:9000"
    //   }
    //   steps {
    //     withCredentials([string(credentialsId: 'sonar', variable: 'SONAR_AUTH_TOKEN')]) {
    //       sh 'cd java-maven-sonar-argocd-helm-k8s/spring-boot-app && mvn sonar:sonar -Dsonar.projectKey=maven -Dsonar.projectName=maven -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
    //     }
    //   }
    // }

      // stage('Build & Deploy') {
      //     steps {
      //         withCredentials([usernamePassword(
      //             credentialsId: 'artifactory-admin',
      //             usernameVariable: 'ARTIFACTORY_USER',
      //             passwordVariable: 'ARTIFACTORY_PASSWORD'
      //         )]) {
      //             configFileProvider([configFile(
      //                 fileId: 'maven-local',
      //                 variable: 'MAVEN_SETTINGS'
      //             )]) {
      //                 sh 'cd java-maven-sonar-argocd-helm-k8s/spring-boot-app; mvn clean deploy -Drevision=${RELEASE_VERSION} -s $MAVEN_SETTINGS'
      //             }
      //         }
      //     }
      // }
       stage('Build & Deploy') {
            steps {
                script {
                    def server = Artifactory.server('artifactory')

                    def buildInfo = Artifactory.newBuildInfo()
                    buildInfo.env.capture = true

                    server.runMaven(
                        pom: 'pom.xml',
                        goals: 'clean deploy',
                        buildInfo: buildInfo
                    )

                    server.publishBuildInfo(buildInfo)
                }
            }
        }
  }
}
