pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('df2a55fc-0d9d-407d-bea8-625c50fc945a') 
        DOCKER_HUB_REPO = 'i211168/my-app' 
    }
    stages {
        stage('i211168 Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/NUCESFAST/scd-final-lab-exam-MaleehaYounas' 
            }
        }
        stage('i211168 Build Backend - Auth') {
            steps {
                dir('Auth') {
                    script {
                        bat 'npm install'
                        bat 'docker build -t %DOCKER_HUB_REPO%:auth .'
                    }
                }
            }
        }
        stage('i211168 Build Backend - Classrooms') {
            steps {
                dir('Classrooms') {
                    script {
                        bat 'npm install'
                        bat 'docker build -t %DOCKER_HUB_REPO%:classrooms .'
                    }
                }
            }
        }
        stage('i211168 Build Backend - Post') {
            steps {
                dir('Post') {
                    script {
                        bat 'npm install'
                        bat 'docker build -t %DOCKER_HUB_REPO%:post .'
                    }
                }
            }
        }
        stage('i211168 Build Backend - Event Bus') {
            steps {
                dir('event-bus') {
                    script {
                        bat 'npm install'
                        bat 'docker build -t %DOCKER_HUB_REPO%:event-bus .'
                    }
                }
            }
        }
        stage('i211168 Push Images to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('', 'DOCKER_HUB_CREDENTIALS') {
                        bat 'docker push %DOCKER_HUB_REPO%:frontend'
                        bat 'docker push %DOCKER_HUB_REPO%:auth'
                        bat 'docker push %DOCKER_HUB_REPO%:classrooms'
                        bat 'docker push %DOCKER_HUB_REPO%:post'
                        bat 'docker push %DOCKER_HUB_REPO%:event-bus'
                    }
                }
            }
        }
       
    }
    post {
        always {
            script {
                bat 'docker-compose down'
            }
        }
    }
}
