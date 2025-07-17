pipeline {
    agent { label 'cind-rg' }
    
    stages{
        stage('code'){
            steps {
                git url: 'https://github.com/mukeshjadav2025/node-todo-labapp-cicd.git', branch: 'main'
            }
        }
        stage('Build and Test'){
            steps {
                sh 'docker build . -t mukeshjadav7696/node-todo-labapp-cicd:latest'
            }
        }
        stage('Login and Push Image'){
            steps {
                echo 'logging in to docker hub and pushing image..'
                withCredentials([usernamePassword(credentialsId:'DockerHub',passwordVariable:'DockerHubPassword', usernameVariable:'DockerHubUsername')]) {
                    sh "docker login -u ${env.DockerHubUsername} -p ${env.DockerHubPassword}"
                    sh "docker push mukeshjadav7696/node-todo-labapp-cicd:latest"
                }    
            }
        }
        stage('Deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
