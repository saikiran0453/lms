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

                echo 'Releasing'
                sh "zip webapp/dist-'${packageJSONVersion}'.zip -r webapp/dist"
                sh "curl -v -u admin:sai123 --upload-file webapp/dist-'${packageJSONVersion}'.zip http://44.217.109.107:8081/repository/lms/"

            }
        }
    }   
        stage('Deploy') { 
            steps {
                script {
                def packageJSON = readJSON file: 'webapp/package.json'
                def packageJSONVersion = packageJSON.version
                echo 'Deploying...' 
                sh "curl -u admin:sai123 -X GET \'http://44.217.109.107:8081/repository/lms/dist-${packageJSONVersion}.zip\' --output dist-'${packageJSONVersion}'.zip"
                sh 'sudo rm -rf /var/www/html/*'
                sh "sudo unzip -o dist-'${packageJSONVersion}'.zip"
                sh "sudo cp -r webapp/dist/* /var/www/html/"
                }   

            }
        }
    }
}