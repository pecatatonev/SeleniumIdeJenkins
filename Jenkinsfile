pipeline {
    agent any
    environment {
        CHROME_VERSION = '89.0.4389.90'
        CHROMEDRIVER_VERSION = '89.0.4389.23'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: "https://github.com/pecatatonev/SeleniumIdeJenkins.git"
            }
        }
        stage('Set up .NET Core') {
            steps {
                bat 'dotnet --version'
            }
        }
        stage('Restore Dependencies') {
            steps {
                bat 'dotnet restore'
            }
        }
        stage('Build') {
            steps {
                bat 'dotnet build Selenium.sln --configuration Release'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'dotnet test'
            }
        }
    }
}
