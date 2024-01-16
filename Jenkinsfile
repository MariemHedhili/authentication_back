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
        
        stage('Build') {
            steps {
                script {
                    withGradle(gradle: 'gradle') {
                        sh 'gradle clean build'
                    } 
                }
            } 
        } 
        
      
    }
    }     

