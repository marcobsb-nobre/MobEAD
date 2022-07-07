pipeline {  
    environment {
      tagName = "marcos_nobre_unyleya"
    }
    agent any 
    stages { 
       stage('SonarQube analysis') {
            steps{
                script{
                    def scannerHome = tool 'sonarscan';
                    withSonarQubeEnv('sonarqube') {
                        sh "${tool("sonarscan")}/bin/sonar-scanner \
                            -Dsonar.projectKey=marcos_nobre_unyleya \
                            -Dsonar.projectName=marcos_nobre_unyleya"
                    }
                }
            }
        }
        stage('Build image') {
            steps{
                script {
                    dockerImage = docker.build tagName + ":$BUILD_NUMBER"
                }
            }
        }
        
    } 
}