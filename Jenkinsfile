pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git credentialsId: 'github-creds', url: 'https://github.com/divyeshx07/ToDoApp-2.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                bat 'npm install'
                bat 'npm run build'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    bat 'scp -o StrictHostKeyChecking=no -r ./build ubuntu@<EC2-IP>:/home/ubuntu/app'
                    bat 'ssh -o StrictHostKeyChecking=no ubuntu@<EC2-IP> "cd /home/ubuntu/app && ./deploy.sh"'
                }
            }
        }
    }
}
