pipeline {
    agent any
    stages {
        stage ('Build Servlet Project') {
            steps {
                bat 'mvn clean package'
                // sh 'mvn clean package'

                // echo 'Initializing the code file'
            }
            
            post{
                success{
                    echo 'Now Archiving....'

                    archiveArtifacts artifacts : '**/*.war' 
                }
            }
        }

        stage ('Deploy build in staging area'){
            steps{
                build job : 'Deploy-StagingArea-Pipeline'
            }
        }

        stage ('Deploy To Production'){
            steps{
                timeout (time: 5, unit: 'Days'){
                    input message: 'Approve DEPLOYMENT Deployment'
                }

                build job : 'Deploy-Production-Pipeline'
            }

            post{
                success{
                    echo 'Deploy on Production is success'
                }

                failure{
                    echo 'Deploy failure on Production'
                }
            }

        }
    }
}
