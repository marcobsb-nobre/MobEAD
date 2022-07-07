pipeline {  
    environment {
      registry = "osanamgcj/mobead_image_build"
      registryCredential = 'dockerhub'
      dockerImage = ''
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
    } 
}