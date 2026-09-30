pipeline {
    agent any

    stages {

        stage('Clone GitHub Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/prajapati200/devops-assignment.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t devops-assignment .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker stop devops-app || exit /b 0'
                bat 'docker rm devops-app || exit /b 0'
                bat 'docker run -d -p 8080:80 --name devops-app devops-assignment'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat '"C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe" -NoProfile -Command "$r=Invoke-WebRequest -Uri http://localhost:8080 -UseBasicParsing; if ($r.StatusCode -ne 200) { exit 1 }"'
            }
        }
    }
}