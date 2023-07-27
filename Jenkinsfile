pipeline {
    agent any 
    stages {
        stage('Test') { 
            steps {
                echo 'Sonar analysis'
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://35.169.182.91:9000" -e SONAR_LOGIN="sqp_41d41460899bb612e5c415c7fbac6b547bd61052"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=sai'
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