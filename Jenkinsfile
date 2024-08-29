pipeline {
    agent any
    tools {
        nodejs 'nodejs'
    }
    stages {
        stage('Build') {
            steps {
                echo "Ejecutar npm install" 
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo "Ejecutar npm test push" 
                sh 'npm test'
            }
        }

        stage('Start Server') {
            steps {
                echo "Starting the server"
                sh 'npm start &'
                sleep 10 
            }
        }

        stage('Make Request') {
            steps {
                echo "Making a request to the server"
                script {
                    def response = sh(script: "curl -o /dev/null -s -w \"%{http_code}\" http://localhost:3000", returnStdout: true).trim()
                    if (response == '200') {
                        echo "Request successful: HTTP 200 OK"
                    } else {
                        error "Request failed with HTTP status: ${response}"
                    }
                }            
            }
        }
    }
}
