pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/Emkloud/maven-job.git'
            }
        }
        stage("SonarQube Analysis") {
            steps {
               withSonarQubeEnv('sonar') {
                  sh 'mvn -f SampleWebApp/pom.xml clean package sonar:sonar'
               } 
            }
        }
        stage("Quality Gate") {
            steps {
              waitForQualityGate abortPipeline: true, credentialsId: '	Sonar-Token'
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

        stage('Deploy to JFrog') {
            steps {
                    rtUpload (
                        serverId: 'my-jfrog',
                        spec: '''{​​​​​​
                             "files": [
                                 {​​​​​​​​​​​​​
                                 "pattern": "**/*.war",
                                "target": "my-repo/"
                                }
                            ]
                            
                        }''',
                        
                    )
                    
            }
                
        }        ​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
                            
                        ​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'devops', 
                path: '', 
                url: 'http://3.87.119.57:8080/')], 
                contextPath: 'pipeline',
                war: '**/*.war'
            }
        }
    }
}
