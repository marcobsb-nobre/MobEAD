pipeline {  
    environment {
      registry = "osanamgcj/mobead_image_build"
      registryCredential = 'dockerhub'
      dockerImage = ''
    }
    agent any 
    stages { 
       stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "./gradlew sonarqube"
                }
            }
        }
    } 
}