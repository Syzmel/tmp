pipeline {
    agent any
       environment {
       SONAR_TOKEN = '8bf909351a6f8d1ad0c61bdf9607d732b5c9a043'
       AWS_REGION = 'ap-southeast-2' // Change based on your setup
        AWS_APP_NAME = 'Ardavan'
        AWS_ENV_NAME = 'Ardavan-env'
    }       
    stages {
        stage('Build') {
            steps {
                bat 'mvn clean compile' // Windows-friendly Maven command
                
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test' // Runs JUnit tests
            }
        }

        stage('Publish Test Results') {
            steps {
                junit '**/target/surefire-reports/*.xml' // Publishes test reports
            }
        }
        stage('SonarCloud Analysis') {
            steps {
                                bat '''
                  sonar-scanner ^
                  -Dsonar.projectKey=Syzmel_tmp ^
                  -Dsonar.organization=sit223 ^
                  -Dsonar.sources=. ^
                  -Dsonar.java.binaries="C:\\tmp\\spring-petclinic"
                  -Dsonar.host.url=https://sonarcloud.io ^
                  -Dsonar.login=8bf909351a6f8d1ad0c61bdf9607d732b5c9a043
                  if %ERRORLEVEL% NEQ 0 exit /b 0
                '''
              }
            }
        stage('Snyk Security Scan') {
            steps {
                script {
                    def snykTokenId = '0fd70700-dcdd-4e80-a424-85129e1d5c55'
                    // ... other Snyk build step configurations ...
                }
            }
        }  
        stage(''Deploy'') {
            steps {
                bat 'docker build -t myapp:latest .'
                bat 'docker run -d -p 8080:8080 myapp:latest'
                }
            }
        }  
    }

