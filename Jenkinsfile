pipeline {
    agent any 
    tools {
        maven 'MAVEN3' 
    }
    triggers {
        cron('H/10 * * * 1') // Triggers every 10 minutes on Mondays
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'mvn clean package'
                }
            }
        }
        stage('Code Coverage') {
            steps {
                script {
                    sh 'mvn jacoco:report'
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/jacoco/jacoco.xml', allowEmptyArchive: true
        }
    }
}
