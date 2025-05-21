pipeline {
    //agent any  // Runs on any available agent
    agent {
        dockerfile {
            filename "Dockerfile.agent-python"
            additionalBuildArgs "-t jenkins-python-agent"
        }
    }

    stages {
        stage('Build') {
            steps {
                echo '🔧 Building the application...'
                // Example: install dependencies or compile
                sh 'echo Build step completed'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                // Example: run unit tests
                sh 'python3 hello.py'
                sh 'echo Running tests...'
                // Replace with your test command, e.g., pytest or npm test
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying application...'
                // Example: docker-compose up or rsync to server
                sh 'echo Deploy step completed'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}
