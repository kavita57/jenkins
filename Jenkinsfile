pipeline {
    agent any

    triggers {
        // Poll the Git repository every 5 minutes for changes
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Building the code using Maven...'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Running unit and integration tests...'

            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Performing static code analysis...'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Performing security scan...'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploying to the staging environment...'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Running integration tests on staging...'

            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploying to the production environment...'
            }
        }
    }
}
