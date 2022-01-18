pipeline {
    agent any
    environment {
        //once you create ACR in Azure cloud, use that here
        registryName = "azureregistryjenkins"
        //- update your credentials ID after creating credentials for connecting to ACR
        registryCredential = 'ACR'
        dockerImage = ''
        registryUrl = 'azureregistryjenkins.azurecr.io' 
    }
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/NguyenThang68/newhelloworld.git'
            }
        }
        stage('Buil stage'){
            steps {
                // This step should not normally be used in your script. Consult the inline help for details.
                withDockerRegistry(credentialsId: 'ACR', url: 'https://azureregistryjenkins.azurecr.io') {
                    sh 'docker build -t thekop68/nodejs:v5 .'
                    sh 'docker tag thekop68/nodejs:v5 azureregistryjenkins.azurecr.io/nodejs:v1'
                    sh 'docker push azureregistryjenkins.azurecr.io/nodejs:v1'
                    sh 'docker run -d -p 8081:8081 --name nodejscacr azureregistryjenkins.azurecr.io/nodejs:v1'
                }
            }
        }
    }
}