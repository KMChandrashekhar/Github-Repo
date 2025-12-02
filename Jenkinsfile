pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/<yourname>/<yourrepo>.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                    if [ $(docker ps -aq -f name=myapp) ]; then
                        docker rm -f myapp
                    fi
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name myapp myapp:latest'
            }
        }
    }

    post {
        success {
            echo "🎉 App deployed successfully!"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}
