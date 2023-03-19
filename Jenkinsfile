pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    sh 'pwd'
                    sh 'ls -lhrt'
                    sh 'cd target'
                    sh 'ls -lhrt'
                    archiveArtifacts artifacts: 'target/*.war'
                    
                }
            }
        }
        stage('Deploy in Staging Environment'){
            steps{
                build job: 'Deploy_Application_Staging_Env'

            }
            
        }
        stage('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }
                build job: 'Deploy_Application_Prod_Env'
            }
        }
    }
}
