pipeline{
    agent any
    environment{
        registry = '154265/fronten-angular'
        registryCredential = 'dockerhub-credentials'
        dockerImage = ''
    }
    
    stages {
        stage('Cloning repository'){
            steps{
                checkout scm
            }
        }


        stage('Build image'){
            steps{
                script{
                    dockerImage = docker.build(registry + "${env.BUILD_NUMBER}")
                }
            }
        }

        stage('push image to registry'){
            steps{
                script{
                    docker.withRegistry('', 'dockerhub-credentials') {
                        dockerImage.push("${env.BUILD_NUMBER}")
                        dockerImage.push('latest')
                        
                    }
                }
            }
        }

        

    }

}