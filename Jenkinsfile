pipeline {
    agent any
    tools{
       maven 'Maven'
    }

    triggers {
        cron('H(0-59)/10 * * * 1')
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Code Coverage') {
            steps {
                sh 'mvn jacoco:prepare-agent test jacoco:report'
            }
            post {
                always {
                    jacocoPublish()
                }
            }
        }
    }
}
