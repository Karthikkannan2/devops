pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }

        stage('Deploy Frontend') {
            steps {
                echo 'Starting local web server for the frontend...'
                // Launches the server in the background and redirects all output to a log file
                bat 'cd src/main/webapp && start /B python -m http.server 8000 > server.log 2>&1'
                // Gives the server 2 seconds to initialize before finishing the pipeline
                bat 'timeout /t 2 /nobreak'
                echo 'Frontend is now live at http://localhost:8000'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }

        failure {
            echo 'Build failed!'
        }
    }
}