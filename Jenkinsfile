pipeline {
    agent any
       environment {
       SONAR_TOKEN = '8bf909351a6f8d1ad0c61bdf9607d732b5c9a043'
       DOCKER_USERNAME = 'sit223'
       DOCKER_TOKEN = 'dckr_pat_72QBxkLhWcJj0-hsl7BE4zGBOL4'    
       IMAGE_NAME = 'sit223/ardavan'     
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
        stage('Deploy') {
            steps {
                script{
                    bat "echo %DOCKER_TOKEN% | docker login -u %DOCKER_USERNAME% --password-stdin"
                    // Pull the Jenkins image
                    bat "docker pull jenkins/jenkins"

                    // Run the Jenkins container
                    bat "docker run -d -p 8080:8080 --name jenkins-server jenkins/jenkins"

                    // Deploy your custom image
                    bat "docker run -d -p 8081:8081 --name my-app %IMAGE_NAME%"
                           
           }                  
        }
      }
   }  
}

