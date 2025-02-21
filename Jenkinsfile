pipeline {
    agent any
    environment {
        CHROME_VERSION = '89.0.4389.90'
        CHROMEDRIVER_VERSION = '89.0.4389.23'
    }
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Set up .NET Core') {
            steps {
                bat 'dotnet --version'
            }
        }
        stage('Uninstall Current Chrome') {
            steps {
                bat 'wmic product where "name like \'%Google Chrome%\'" call uninstall /nointeractive'
            }
        }
        stage('Install Specific Version of Chrome') {
            steps {
                bat "curl -L -o chrome_installer.exe https://dl.google.com/chrome/install/${CHROME_VERSION}/chrome_installer.exe"
                bat "chrome_installer.exe /silent /install"
            }
        }
        stage('Download and Install ChromeDriver') {
            steps {
                bat "curl -L -o chromedriver_win32.zip https://chromedriver.storage.googleapis.com/${CHROMEDRIVER_VERSION}/chromedriver_win32.zip"
                bat 'powershell -Command "Expand-Archive -Path chromedriver_win32.zip -DestinationPath . -Force"'
            }
        }
        stage('Restore Dependencies') {
            steps {
                bat 'dotnet restore'
            }
        }
        stage('Build') {
            steps {
                bat 'dotnet build --configuration Release'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'dotnet test'
            }
        }
    }
}
