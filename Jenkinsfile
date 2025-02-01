pipeline{
    agent any

    stages{
        stage('docker install'){
            steps{ 
                echo 'docker installed'
                sh 'docker --version'
            }
        }
        stage('pull'){
            steps{ 
                sh 'docker pull nginx'
            }
        }
        stage('run'){
            steps{
                sh 'docker run -it -d --name chandu -p 8000:80 nginx'
            }
        }
        stage('backup'){
            steps{
                sh 'docker commit chandu backup'
            }
        }
        stage('tag'){
            steps{
                sh 'docker tag backup kulashekaralwarn/mock3'
            }
        }
        stage('push'){
            steps{
                 sh 'echo "@docker#123" | docker login -u "kulashekaralwarn" --password-stdin'
                sh 'docker push kulashekaralwarn/mock3'
            }
        }
    }
    post{
        always{
            sh 'docker rmi -f nginx'
        }
        success{
            sh 'docker rm -f chandu'
        }
    }
    
}