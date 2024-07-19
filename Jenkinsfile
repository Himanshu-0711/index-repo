pipeline {
    agent any
    
    environment {
        NGINX_SERVER = '3.80.87.51' // Replace with your Nginx server IP or hostname
        NGINX_USER = 'ubuntu' // Nginx server user with write permissions
        NGINX_HTML_PATH = '/var/www/html/' // Path where Nginx serves static content
        GIT_REPO_URL = 'https://github.com/Himanshu-0711/index-repo.git' // GitHub repo URL (added .git suffix)
        GIT_BRANCH = 'main' // Branch from which to deploy
    }
    
    stages {
        stage('Checkout') {
            steps {
                cleanWs() // Clean workspace before checking out
                git branch: "${GIT_BRANCH}", url: "${GIT_REPO_URL}" // Checkout from GitHub
            }
        }
        
        stage('Build') {
            steps {
                // If any build steps are needed (e.g., npm install, yarn build), add them here
            }
        }
        
        stage('Deploy to Nginx') {
            steps {
                // Copy the contents of the checked-out repository to Nginx HTML directory
                script {
                    sh "sudo cp -r ./* ${NGINX_HTML_PATH}/"
                }
            }
        }
        
        stage('Post Deployment') {
            steps {
                // Perform any post-deployment actions if needed (e.g., reload Nginx)
                script {
                    sh "sudo systemctl reload nginx"
                }
            }
        }
    }
    
    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
