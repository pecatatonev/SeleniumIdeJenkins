pipeline {
    agent any
    environment {
        CHROME_VERSION = '89.0.4389.90'
        CHROMEDRIVER_VERSION = '89.0.4389.23'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/pecatatonev/SeleniumIdeJenkins'
            }
        }
        stage('Set up .NET Core') {
            steps {
                bat 'dotnet --version'
            }
        }
        stage('List Workspace Files') {
            steps {
                bat 'dir'
            }
        }
        stage('Restore Dependencies') {
            steps {
                bat 'dotnet restore'
            }
        }
        stage('Clean Build') {
            steps {
                bat 'dotnet clean SeleniumIde.sln'
                bat 'dotnet build SeleniumIde.sln --configuration Release'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'dotnet test'
            }
        }
    }
}
