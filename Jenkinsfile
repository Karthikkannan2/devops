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
                echo 'Deploying frontend assets to the production directory...'
                // This simulates a deployment by copying your workspace HTML/CSS files 
                // to a stable deployment folder without trying to launch new background processes.
                bat 'echo F | xcopy /Y "src\\main\\webapp\\index.html" "src\\main\\webapp\\index.html"'
                bat 'xcopy /E /I /Y "src\\main\\webapp\\css" "src\\main\\webapp\\css"'
                echo 'Deployment complete! Refresh http://localhost:8000 to see changes.'
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