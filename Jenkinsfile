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

        stage('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }
                  
                  sh 'scp target/*.war vagrant@192.168.2.49:/opt/wildfly/standalone/deployments/' 
            
            }
        }
    }
}
