pipeline {
    agent any 

    stages {
        stage('Test') { 
            steps {
                echo 'sonar analysis' 
            }
        }
        stage('Build & release') { 
            steps {
                echo 'Building' 
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Deploying...' 
            }
        }
    }
}