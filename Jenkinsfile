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
                    sh 'gradle init'
                    sh "echo 'building..'"
                    withGradle {
                   sh 'gradle wrapper build'
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
                withSonarQubeEnv(installationName: 'SonarServer', credentialsId: 'sonar-credentials') {
                     sh '$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=$PROJECT_NAME -Dsonar.java.binaries=build/classes/'
                }
             }
        }             
            
    }
}
