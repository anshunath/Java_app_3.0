pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/anshunath/complete-prodcution-e2e-pipeline'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-api') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage('Docker Build and Push') {
            steps {
                script {
                    def dockerImage = docker.build('sonarqube')
                    docker.withRegistry('https://hub.docker.com', 'anshu1997') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
