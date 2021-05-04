pipeline {
    agent any
    
    tools {
        maven 'maven'
        jdk 'jdk'
    }
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Staging'){
            steps {
                build job: 'deploy to staging'
            }
        }

        stage ('Deploy to Production'){
            steps{
                timeout(time:180, unit:'SECONDS'){
                    input message:'Approve PRODUCTION Deployment?',
                }

                build job: 'Deploy to prod'
            }
            post {
                success {
                    echo 'Code deployed to Production.'
                }

                failure {
                    echo ' Deployment failed.'
                }
            }
        }


    }
}
