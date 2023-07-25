pipeline {
    agent any 

    stages {
        stage('Test') { 
            steps {
                echo 'sonar analysis' 
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://44.217.109.107:9000" -e SONAR_LOGIN="sqp_f4931740bbaa62f391f1d85cd118722c08153ead"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        stage('Build & release') { 
            steps {
                script {
                def packageJSON = readJSON file: 'webapp/package.json'
                def packageJSONVersion = packageJSON.version
                sh "echo '${packageJSONVersion}'"

                echo 'Building' 
                sh 'cd webapp && npm install && npm run build'
                sh 'cd webapp && ls dist'
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Deploying...' 
            }
        }
    }
}