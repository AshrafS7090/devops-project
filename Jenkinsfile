pipeline {

    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                echo '===== Building Docker Image ====='

                sh 'docker build -t devops-app:2.0 -f docker/Dockerfile .'
            }
        }

        stage('Stop Old Container') {
            steps {
                echo '===== Stopping Old Container ====='

                sh 'docker stop devops-web || true'
            }
        }

        stage('Remove Old Container') {
            steps {
                echo '===== Removing Old Container ====='

                sh 'docker rm devops-web || true'
            }
        }

        stage('Deploy New Container') {
            steps {
                echo '===== Starting New Container ====='

                sh 'docker run -d --name devops-web -p 80:80 devops-app:2.0'
            }
        }

        stage('Health Check') {
            steps {
                echo '===== Waiting for Application ====='

                sleep 5

                echo '===== Testing Application ====='

                sh 'curl -f http://localhost'
            }
        }
    }

    post {
        success {
            echo '===== CI/CD PIPELINE SUCCESSFUL ====='
        }

        failure {
            echo '===== CI/CD PIPELINE FAILED ====='
        }
    }
}
