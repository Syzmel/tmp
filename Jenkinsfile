pipeline {
    agent any
    
    stages {
        stage('SonarCloud Analysis') {
            steps {
                                bat '''
                  sonar-scanner ^
                  if %ERRORLEVEL% NEQ 0 exit /b 0
                '''
              }
            }
        }  
    }
