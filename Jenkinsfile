pipeline{
    agent{
        label 'JenkinsAgent'
    }
    tools{
        maven 'maven3'
        jdk 'java17'
    }
    stages{
        stage('Cleanup'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout'){
            steps{
                git branch: 'main' ,credentialsId: 'github-token' ,url: 'https://github.com/chait21/register-app_from_Ashfaque.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test'
            }
        }
    }
}