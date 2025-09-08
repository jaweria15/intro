pipeline {
    agent any

    environment {
        GIT_CREDENTIALS_ID = '	github-token' // Jenkins me save kiya hua GitHub credentials ka ID
        REPO_URL = 'https://github.com/jaweria15/intro.git'
        BRANCH = 'main'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: "${BRANCH}", credentialsId: "${GIT_CREDENTIALS_ID}", url: "${REPO_URL}"
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Project') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Commit & Push Changes') {
            steps {
                bat '''
                    git config --global user.email "javeriaf322@gmail.com"
                    git config --global user.name "Jaweria"
                    git add .
                    git commit -m "Automated build from Jenkins" || exit 0
                    git push origin %BRANCH%

                '''
            }
        }
    }
}
