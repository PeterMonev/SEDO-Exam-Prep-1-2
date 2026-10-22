
pipeline {
    agent any

    options {
        skipDefaultCheckout()
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Environment') {
            steps {
                bat 'dotnet --info'
            }
        }

        stage('Restore') {
            steps {
                bat 'dotnet restore SoftUniBazar.sln'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build SoftUniBazar.sln -c Release --no-restore'
            }
        }

        stage('Unit Tests') {
            steps {
                bat 'dotnet test SoftUniBazar.Tests/SoftUniBazar.Tests.csproj -c Release --no-build'
            }
        }

        stage('Integration Tests') {
            steps {
                bat 'dotnet test SoftUniBazar.IntegrationTests/SoftUniBazar.IntegrationTests.csproj -c Release --no-build'
            }
        }
    }

    post {
        success {
            echo 'SoftUniBazar CI completed successfully!'
        }

        failure {
            echo 'SoftUniBazar CI failed. Check the build logs.'
        }
    }
}
