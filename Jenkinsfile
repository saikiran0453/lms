pipeline {
    agent any 
    stages {
        stage('Test') { 
            steps {
                echo 'sonar analysis'
            }
        }
        stage('Build & Release') { 
            steps {
                echo 'Building'
            }
        }
        stage('Deploy') { 
            steps {
                echo "Deploying"
            }
        }
    }
} 