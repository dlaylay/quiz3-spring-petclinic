pipeline {
    agent any 
    tools {
        maven 'MAVEN3' // Use the name you provided in the Global Tool Configuration
    }
    triggers {
        cron('H/10 * * * 1') // Triggers every 10 minutes on Mondays
    }
    stages {
        stage('Build') {
            steps {
                script {
                    // Use `sh` for Unix/Linux or `bat` for Windows
                    if (isUnix()) {
                        sh 'mvn clean package'
                    } else {
                        bat 'mvn clean package'
                    }
                }
            }
        }
        stage('Code Coverage') {
            steps {
                script {
                    // Use `sh` for Unix/Linux or `bat` for Windows
                    if (isUnix()) {
                        sh 'mvn jacoco:report'
                    } else {
                        bat 'mvn jacoco:report'
                    }
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
