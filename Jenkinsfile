pipeline {
    agent any

    triggers {
        cron('H/10 * * * 4')
    }

    tools {
        maven 'maven'
    }

    stages {
        stage('Build') {
            steps {
                tool 'Maven'
                sh 'mvn clean package'
            }
        }

        stage('Test with JaCoCo') {
            steps {
                tool 'Maven'
                sh 'mvn test jacoco:report'
            }

            post {
                always {
                    jacoco execPattern: '**/target/jacoco.exec', classPattern: '**/classes', sourcePattern: '**/src/main/java'
                }
            }
        }
    }

    post {
        success {
            echo 'Build was successful!'
        }

        failure {
            echo 'Build failed.'
        }
    }
}
