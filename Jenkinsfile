pipeline {
    agent any

    environment {
        DOTNET_CLI_HOME = "${WORKSPACE}"
        PUBLISH_DIR = 'out'
        PROJECT_PATH = 'TodoApi.csproj'  // ✅ your actual file
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
                // Optional: only if you add a test project later
                echo "No test project found. Skipping for now."
            }
        }

        stage('Publish App') {
            steps {
                bat "dotnet publish %PROJECT_PATH% -c Release -o %PUBLISH_DIR%"
            }
        }

        stage('Deploy (Optional)') {
            steps {
                echo "✅ App ready in %PUBLISH_DIR%. Add deployment step if needed (e.g., xcopy to IIS)."
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
