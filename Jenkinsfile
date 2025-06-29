pipeline {
    agent any

    environment {
        DOTNET_ROOT = '/usr/local/share/dotnet'
        PATH = "${DOTNET_ROOT}:${PATH}"
    }

    stages {
        stage('Restore') {
            steps {
                echo 'Restoring dependencies...'
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the solution...'
                sh 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
    }

    post {
        always {
            echo "Pipeline completed for branch: ${env.BRANCH_NAME}"
        }
        success {
            echo '✅ Build and tests succeeded!'
        }
        failure {
            echo '❌ Pipeline failed. Please check the logs!'
        }
    }
}
