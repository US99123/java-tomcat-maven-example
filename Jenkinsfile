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
    }
}
