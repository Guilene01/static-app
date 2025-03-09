pipeline{
    agent { label 'java'
    }
    stages{
        stage('DockerLogin'){
            steps{
                sh 'aws ecr get-login-password --region us-east-1 | \
                docker login --username AWS \
                --password-stdin 977098999802.dkr.ecr.us-east-1.amazonaws.com'
                
                
            }

        }
        stage('DockerBuild'){
            steps{
                sh 'docker build -t dev .'
                sh 'docker build -t newversion .'
                sh 'docker images'
                
            }

        }
        stage('DockerTag'){
            steps{
                sh 'docker tag dev:latest 977098999802.dkr.ecr.us-east-1.amazonaws.com/dev:latest'
                sh 'docker tag dev:latest 977098999802.dkr.ecr.us-east-1.amazonaws.com/dev:v1.$BUILD_NUMBER'
                
                
            }

        }
        stage('DockerPush'){
            steps{
                sh 'docker push 977098999802.dkr.ecr.us-east-1.amazonaws.com/dev:latest'
                sh 'docker push 977098999802.dkr.ecr.us-east-1.amazonaws.com/dev:v1.$BUILD_NUMBER'
                
                
            }

        }
        stage('Testing'){
            steps{
                sh 'docker images'
                sh 'docker run -itd --name web1 -p 80:80 webapp'
                sh 'docker ps'
                
            }

        }
        
        
    }
}