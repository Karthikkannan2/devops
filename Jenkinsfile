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
                // This changes directory to your webapp folder and starts a background Python server on port 8000
                bat 'cd src/main/webapp && start /B python -m http.server 8000'
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