pipeline {  
    environment {
      tagName = "marcos_nobre_unyleya"
      containerName = "aplicacao_ead"
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
                            -Dsonar.projectKey=marcos_nobre_unyleya_${params.environment} \
                            -Dsonar.projectName=marcos_nobre_unyleya_${params.environment}"
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
        stage('Deploy container') {
            steps {
                script {
                    def fullName = """${containerName}_${params.environment}"""
                    sh  """
                        docker stop ${fullName} || true && \
                        docker rm ${fullName} || true && \
                        docker run -d --name ${fullName} \\
                        -p ${params.port}:80 \\
                        ${tagName}:$BUILD_NUMBER
                    """
                }
            }
        }
    } 
}