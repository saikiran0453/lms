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

                echo 'Releasing'
                sh "zip webapp/dist-'${packageJSONVersion}'.zip -r webapp/dist"
                sh "curl -v -u admin:dev123 --upload-file webapp/dist-'${packageJSONVersion}'.zip http://35.169.182.91:8081/repository/sai/"
                    

                }   
            }
        }
        stage('Deploy') { 
            steps {
                script {
                def packageJSON = readJSON file: 'webapp/package.json'
                def packageJSONVersion = packageJSON.version

                echo "Deploying"
                sh "curl -u admin:dev123 -X GET \'http://35.169.182.91:8081/repository/sai/dist-${packageJSONVersion}.zip\' --output dist-'${packageJSONVersion}'.zip"
                sh 'sudo rm -rf /var/www/html/*'
                sh "sudo unzip -o dist-'${packageJSONVersion}'.zip"
                sh "sudo cp -r webapp/dist/* /var/www/html/"
                
                }
            }
        }
    }
} 