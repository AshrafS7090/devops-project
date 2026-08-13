pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                echo '===== Building Docker Image ====='
                sh 'docker build -t devops-app:2.0 -f docker/Dockerfile .'
            }
        }

        stage('Deploy Container') {
            steps {
                echo '===== Deploying Application ====='

                sh '''
                    docker stop devops-web || true
                    docker rm devops-web || true
                    docker run -d --name devops-web -p 80:80 devops-app:2.0
                '''
            }
        }

        stage('Test Application') {
            steps {
                echo '===== Testing Application ====='

                sh '''
                    sleep 5
                    curl -f http://localhost
                '''
            }
        }
    }
}
