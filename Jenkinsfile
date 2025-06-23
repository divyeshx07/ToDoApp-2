pipeline {
    agent any

    environment {
        DOTNET_CLI_HOME = "$WORKSPACE"
        PUBLISH_DIR = 'out'
    }

    tools {
        dotnet 'dotnet-sdk' // Ensure this matches your Jenkins SDK configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/todo-app.git'
            }
        }

        stage('Restore Dependencies') {
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build --configuration Release --no-restore'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'dotnet test --no-build --verbosity normal'
            }
        }

        stage('Publish App') {
            steps {
                sh 'dotnet publish -c Release -o $PUBLISH_DIR'
            }
        }

        stage('Deploy (Optional)') {
            steps {
                echo "You can add steps here to copy files to a web server or remote machine"
                // Example: copy files to IIS server or shared drive
                // sh 'scp -r $PUBLISH_DIR/* user@yourserver:/var/www/todo-app/'
            }
        }
    }

    post {
        success {
            echo "✅ CI/CD pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed. Please check the logs."
        }
    }
}
