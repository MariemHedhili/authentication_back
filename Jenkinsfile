pipeline{
    

    agent any 
    tools {
      gradle 'gradle'
    }
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/MariemHedhili/authentication_back.git'
                }
            }
        }
        
        stage('Build') {
            steps {
                script {
                    def jdkInstallation = tool name: 'JDK', type: 'hudson.model.JDK'
                    env.PATH = "${jdkInstallation}/bin:${env.PATH}"
                     dir('backend') {
                     sh 'gradle init'
                    //sh "echo 'building..'"
                   
                      withGradle {
                        sh 'gradle wrapper build --scan'
                        sh' pwd'
                        sh 'ls -l'
                        
                      }
                  } 
                }
            } 
        } 
        
      stage('SonarQube Analysis') {
            environment {
                SCANNER_HOME = tool 'SonarQube'
                PROJECT_NAME = "authentication_back"
            }
            
            steps {
                 dir('backend') {
                    
                  withSonarQubeEnv(installationName: 'SonarServer', credentialsId: 'sonar-credentials') {
                     sh '$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=$PROJECT_NAME -Dsonar.java.binaries=build/classes'
                }
            
                 }
            }
        } 
        stage('Upload app to nexus') {
            steps {
                
                sh "tar -czvf backapp.tar.gz ./backend"
                nexusArtifactUploader artifacts: [[artifactId: 'backapp', classifier: '', file: 'backapp.tar.gz', type: 'tar.gz']], credentialsId: 'nexus-credentials', groupId: 'backend', nexusUrl: 'nexus:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'back-repo', version: "1.${env.BUILD_NUMBER}.0"
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dir('backend') {
                        sh "docker build -t meriemhedhili/auth-back:${env.BUILD_NUMBER} ."
                    }
                }
            }
        }
        stage('Push image to DockerHub') {
            
            steps {
                script {
               
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                        sh "echo \${DOCKERHUB_PASSWORD} | docker login -u \${DOCKERHUB_USERNAME} --password-stdin"
                        // Add the docker push step here
                        docker.withRegistry("https://registry.hub.docker.com", 'dockerhub-credentials') {
                            docker.image("${DOCKERHUB_USERNAME}/auth-back:${env.BUILD_NUMBER}").push()
                        }
                    }
                }
            }
            
        } 
        stage('Deploy') {
            steps {
                script {
                   
                    sh "docker-compose up -d"
                }
            }
        }
    }
}
