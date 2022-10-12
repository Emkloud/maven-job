pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/Emkloud/maven-job.git'
            }
        }
        stage('Test the Codes') {
            steps {
                sh 'cd SampleWebApp && mvn test'
            }
        }
        stage('Build by Maven') {
            steps {
                sh 'cd SampleWebApp && mvn package'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'devops', 
                path: '', 
                url: 'http://3.80.60.10:8080')], 
                contextPath: 'pipeline', 
                war: '**/*.war'
            }
        }
    }
}