pipeline{
    

    agent any 
    
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
                    
                      sh './gradlew clean build'
                    
                    }
                }
            }
        }
    }     

