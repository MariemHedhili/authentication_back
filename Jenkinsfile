npipeline{
    

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
                PROJECT_NAME = "backend"
            }
            
            steps {
                withSonarQubeEnv(installationName: 'SonarServer', credentialsId: 'sonar-credentials') {
                sh "./gradlew sonarqube \
                  -Dsonar.projectKey=${PROJECT_NAME} \
                  -Dsonar.host.url=${env.SONAR_HOST_URL} \
                  -Dsonar.login=${env.SONAR_AUTH_TOKEN} \
                  -Dsonar.projectName=${PROJECT_NAME} \
                  -Dsonar.projectVersion=${BUILD_NUMBER}"
                }
             }
        }             
            
    }
}
