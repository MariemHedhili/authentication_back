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
        
      
    }
    }     

