pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git credentialsId: 'github-creds', url: 'https://github.com/divyeshx07/ToDoApp-2.git'

            }
        }

        stage('Build') {
            steps {
                sh 'echo "This is the build step"'
                // e.g., npm install, dotnet build, etc.
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh 'scp -o StrictHostKeyChecking=no -r ./dist ubuntu@<35.176.246.99>:/home/ubuntu/app'
                    sh 'ssh -o StrictHostKeyChecking=no ubuntu@<35.176.246.99> "cd /home/ubuntu/app && ./deploy.sh"'
                }
            }
        }
    }
}
