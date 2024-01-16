pipeline{
    

    agent any 
    tools {
        gradle "gradle"
    }
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/MariemHedhili/authentication_back.git'
                }
            }
        }
        
        stage('Build SpringBoot App') {
            steps {
                script {
                    dir('backend')  
                       sh './gradlew clean build'
                    }
                }
            }
        }
    }     

