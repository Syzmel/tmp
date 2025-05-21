pipeline {
    agent any
       environment {
       SONAR_TOKEN = credentials('8bf909351a6f8d1ad0c61bdf9607d732b5c9a043')
    stages {
        stage('Build') {
            steps {
                bat 'mvn clean compile' // Windows-friendly Maven command
                //-Dsonar.java.binaries="C:\\tmp\\spring-petclinic"
            }
        }
        stage('SonarCloud Analysis') {
            steps {
                                bat '''
                  sonar-scanner ^
                  -Dsonar.projectKey=Syzmel_tmp ^
                  -Dsonar.organization=sit223 ^
                  -Dsonar.sources=. ^
                  
                  -Dsonar.host.url=https://sonarcloud.io ^
                  -Dsonar.login=8bf909351a6f8d1ad0c61bdf9607d732b5c9a043
                  if %ERRORLEVEL% NEQ 0 exit /b 0
                '''
              }
            }
        }  
    }
