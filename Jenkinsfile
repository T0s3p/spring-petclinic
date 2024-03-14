pipeline {
    agent any

    triggers {
        cron('H */10 * * 4') // Trigger every 10 minutes on Thursdays
    }

    tools {
        git 'G3'
        maven 'M3'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout SCM using the specified Git tool
                git branch: 'main', url: 'https://github.com/shawanaGideon/spring-petclinic.git'
            }
        }

        stage('Build Maven Project') {
            steps {
                sh 'mvn clean package' // Use the 'maven' tool from Jenkins to execute Maven commands
            }
        }

        stage('Code Coverage') {
            steps {
                // Run tests with coverage and generate coverage report
                sh 'mvn clean test jacoco:prepare-agent jacoco:report'

                // Archive Jacoco coverage reports
                jacoco(execPattern: 'target/**/*exec')
            }
        }
    }
}
