pipeline {
    agent any

    triggers {
        // Poll the Git repository every 5 minutes for changes
        pollSCM('H/5 * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Building the code using Maven...'
                // Tool: Maven
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Running unit and integration tests...'
                // Tool: JUnit (for unit tests), TestNG or Postman/Newman for integration tests
                sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Performing static code analysis...'
                // Tool: SonarQube
                sh 'mvn sonar:sonar -Dsonar.projectKey=my-project -Dsonar.host.url=http://localhost:9000 -Dsonar.login=your_token'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Performing security scan...'
                // Tool: OWASP Dependency-Check or Snyk
                sh 'dependency-check --project my-project --scan . --format HTML'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploying to the staging environment...'
                // Tool: SCP/SSH or Ansible
                sh 'scp target/myapp.jar ec2-user@staging-ec2:/home/ec2-user/app/'
                sh 'ssh ec2-user@staging-ec2 "java -jar /home/ec2-user/app/myapp.jar &"'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Running integration tests on staging...'
                // Tool: Postman/Newman or custom scripts
                sh 'newman run postman_collection.json'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploying to the production environment...'
                // Tool: SCP/SSH or Ansible
                sh 'scp target/myapp.jar ec2-user@production-ec2:/home/ec2-user/app/'
                sh 'ssh ec2-user@production-ec2 "java -jar /home/ec2-user/app/myapp.jar &"'
            }
        }
    }
}
