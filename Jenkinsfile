pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Harsha-Kyle/Jenkins.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('Harsha_Kyle/python-app')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'H', url: '']) {
                    script {
                        docker.image('Harsha_Kyle/python-app').push('latest')
                    }
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    docker.image('Harsha_Kyle/python-app:latest').inside {
                        sh 'pytest tests/'
                    }
                }
            }
        }
    }
}
