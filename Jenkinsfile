pipeline {
    agent any

    triggers {
        // Poll the Git repository every 2 minutes for changes
        pollSCM('H/1 * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Building the code using Maven...'
                // Tool: Maven
                echo 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Running unit and integration tests...'
                // Tool: JUnit (for unit tests), TestNG or Postman/Newman for integration tests
                echo 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Performing static code analysis...'
                // Tool: SonarQube
                echo 'mvn sonar:sonar -Dsonar.projectKey=my-project -Dsonar.host.url=http://localhost:9000 -Dsonar.login=your_token'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Performing security scan...'
                // Tool: OWASP Dependency-Check or Snyk
                echo 'dependency-check --project my-project --scan . --format HTML'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploying to the staging environment...'
                // Tool: SCP/SSH or Ansible
                echo 'scp target/myapp.jar ec2-user@staging-ec2:/home/ec2-user/app/'
                echo 'ssh ec2-user@staging-ec2 "java -jar /home/ec2-user/app/myapp.jar &"'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Running integration tests on staging...'
                // Tool: Postman/Newman or custom scripts
                echo 'newman run postman_collection.json'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploying to the production environment...'
                // Tool: SCP/SSH or Ansible
                echo 'scp target/myapp.jar ec2-user@production-ec2:/home/ec2-user/app/'
                echo 'ssh ec2-user@production-ec2 "java -jar /home/ec2-user/app/myapp.jar &"'
            }
        }
    }
    post {
        always {
        // Send notification emails at the end of test and security scan stages
        emailext attachLog: true, body: "${currentBuild.result}: ${BUILD_URL}", compressLog:false,
        subject: "Build Notification: ${JOB_NAME}-Build# ${BUILD_NUMBER}${currentBuild.result}", 
        to: 'dkavita2121@gmail.com'
        }
 }
}
