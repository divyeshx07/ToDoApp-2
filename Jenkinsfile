pipeline {
    agent any

    environment {
        DOTNET_CLI_HOME = "${WORKSPACE}"
        PUBLISH_DIR = 'out'
        PROJECT_PATH = 'TodoApi/TodoApi.csproj' // 👉 Replace with actual path to your .csproj
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
                bat "dotnet restore %PROJECT_PATH%"
            }
        }

        stage('Build') {
            steps {
                bat "dotnet build %PROJECT_PATH% --configuration Release --no-restore"
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat "dotnet test %PROJECT_PATH% --no-build --verbosity normal"
            }
        }

        stage('Publish App') {
            steps {
                bat "dotnet publish %PROJECT_PATH% -c Release -o %PUBLISH_DIR%"
            }
        }

        stage('Deploy (Optional)') {
            steps {
                echo "Add deployment logic here if needed"
            }
        }
    }

    post {
        success {
            echo "✅ CI/CD pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed. Please check logs."
        }
    }
}
