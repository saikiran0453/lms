pipeline {
    agent any 
    stages {
        stage('Test') { 
            steps {
                echo 'sonar analysis'
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://35.169.182.91:9000" -e SONAR_LOGIN="sqp_5857cb5f0be6ca72576b868167dc67de0ed7e071"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=sai'
            }
        }
        stage('Build & Release') { 
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
                echo "Deploying"
            }
        }
    }
} 