pipeline {
    agent any
    tools {
        maven 'maven-3.9.11'
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
    }
}
