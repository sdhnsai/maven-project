pipeline {
    agent any
    
    tools {
        maven 'maven'
        jdk 'jdk'
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
                sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"         
            }
        }
    }
}
