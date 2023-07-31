pipeline {
    agent any 
    stages {
        stage('Test') { 
            steps {
                echo 'test' 
                sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://184.73.75.97:9000" -e SONAR_LOGIN="sqp_deeb05362bdb010c865f6deccc3ea2109e60172f"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=pro'
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
                echo 'Deploying' 
            }
        }
    }
}