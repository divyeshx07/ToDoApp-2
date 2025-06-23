pipeline {
    agent any

    environment {
        DOTNET_CLI_HOME = "$WORKSPACE"
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
                sh 'dotnet --version'      // confirm dotnet is installed
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
                echo "You can add custom deployment commands here (e.g., copy to IIS, SCP to server)"
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
