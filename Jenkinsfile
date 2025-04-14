pipeline{
    agent{
        label 'JenkinsAgent'
    }
    tools{
        maven 'maven3'
        jdk 'java17'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
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
        stage('SonarQube Analysis'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'jenkins-sonarqube'){
                    sh "mvn sonar:sonar -Dsonar.projectKey=register-app -Dsonar.host.url=http://18.61.177.240:9000 -Dsonar.login=admin -Dsonar.password=admin123"
                    }
                }
            }
        }
        stage("SonarQube Quality Gate"){
            steps{
                timeout(time: 10, unit: 'MINUTES'){
                    waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-sonarqube'
                }
            }
        }
    }
}