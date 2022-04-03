pipeline{
    agent any
    
    environment {
        registry = "reddymasu/springboot"
        registryCredential = 'docker_hub'
        dockerImage = ''
    }


    stages {
        
        stage('source code check'){
            steps{
                git branch: 'main', url: 'https://github.com/suresh0126/spring_boot.git'
            }
        }
        stage('Build docker image') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 203423047758.dkr.ecr.us-east-1.amazonaws.com'
                sh 'docker build -t spring_boot .'
                sh 'docker tag spring_boot:latest 203423047758.dkr.ecr.us-east-1.amazonaws.com/spring_boot:latest'
                sh 'docker push 203423047758.dkr.ecr.us-east-1.amazonaws.com/spring_boot:latest'
            }
        }
        stage('Remove Unused docker image') {
            steps{
                sh "docker rmi 203423047758.dkr.ecr.us-east-1.amazonaws.com/spring_boot:latest"
            }
        }
        stage('Deployment') { 
            steps { 
               echo 'This is a minimal pipeline.' 
            }
        }
    }
    
}  