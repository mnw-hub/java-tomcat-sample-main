pipeline {
    agent any
    tools {
        maven 'maven-3.8.4'
    }
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo 'Now Archiving the Artifacts.....'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Deploy to Staging Environment') {
            steps {
                build job: 'Deploy-Application-Staging-Environment'
            }
        }
        #stage('Deploy to Production Environment') {
        #    steps {
        #        timeout(time:5, unit:'DAYS') {
        #            input message:'Approve PRODUCTION Deployment?'
        #        }
        #        build job: 'Deploy-Application-Staging-Environment'
        #   }
        # }
    }
}
