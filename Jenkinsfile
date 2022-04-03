pipeline{
    agent any
    
    environment {
        registry = "https://hub.docker.com/springboot"
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
                script {
                    docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Push docker image') { 
            steps{    
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Remove Unused docker image') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
        stage('Deployment') { 
            steps { 
               echo 'This is a minimal pipeline.' 
            }
        }
    }
    
}  