pipeline {
    agent any
    
    stages {
        stage('SonarCloud Analysis') {
            steps {
                                bat '''
                  sonar-scanner ^
                  sonarQubeServerUrl 'http://your-sonarqube-server:9000'
                   if %ERRORLEVEL% NEQ 0 exit /b 0
                '''
              }
            }
        }  
    }
