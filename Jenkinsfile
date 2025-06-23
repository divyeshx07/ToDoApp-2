pipeline {
    agent any

    environment {
        DOTNET_CLI_HOME = "${WORKSPACE}"
        PUBLISH_DIR = 'out'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/divyeshx07/ToDoApp-2.git'
            }
        }

        stage('Restore Dependencies') {
            steps {
                bat 'dotnet --version'
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build --configuration Release --no-restore'
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat 'dotnet test --no-build --verbosity normal'
            }
        }

        stage('Publish App') {
            steps {
                bat 'dotnet publish -c Release -o %PUBLISH_DIR%'
            }
        }

        stage('Deploy (Optional)') {
            steps {
                echo "🔧 Add your deployment steps here (copy to IIS folder, etc.)"
                // Example (optional):
                // bat 'xcopy /Y /E %PUBLISH_DIR% C:\\inetpub\\wwwroot\\ToDoApp'
            }
        }
    }

    post {
        success {
            echo "✅ Build and publish succeeded!"
        }
        failure {
            echo "❌ Pipeline failed."
        }
    }
}
