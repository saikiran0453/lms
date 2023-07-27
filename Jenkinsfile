pipeline {
    agent any 
    stages {
        stage('Test') { 
            steps {
                echo 'Sonar analysis'
            }
        }
        stage('Build & release') { 
            steps {
                echo 'Build'
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Deploying'
            }
        }
    }
}