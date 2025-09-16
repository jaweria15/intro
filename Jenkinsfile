pipeline {
    agent any

    environment {
        GIT_CREDENTIALS_ID = 'github-token' 
        REPO_URL = 'https://github.com/jaweria15/intro.git'
        BRANCH = 'main'
        NETLIFY_AUTH_TOKEN = credentials('NETLIFY_AUTH_TOKEN')
        SITE_ID = 'fa8284ac-61c2-4b3e-ad2f-db958fda78a6'  
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
        

        stage('Deploy to Netlify') {
            steps {
                bat "npx netlify deploy --dir=build --prod --auth=%NETLIFY_AUTH_TOKEN% --site=%SITE_ID%"
            }
        }
    }
}
