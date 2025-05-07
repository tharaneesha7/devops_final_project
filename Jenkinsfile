pipeline {
    agent any

    environment {
        DOCKERHUB_USER = 'tharaneesh'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/tharaneesha7/devops_final_project.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    def services = ['frontend', 'cart', 'product', 'user']
                    for (srv in services) {
                        dir(srv) {
                            sh "docker build -t ${DOCKERHUB_USER}/${srv}:latest ."
                        }
                    }
                }
            }
        }

        stage('Push Docker Images') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    def services = ['frontend', 'cart', 'product', 'user']
                    for (srv in services) {
                        sh "docker push ${DOCKERHUB_USER}/${srv}:latest"
                    }
                }
            }
        }
    }
}
