pipeline {
    agent any
    
    environment {
        // Environment variables
        NGINX_SERVER = '3.80.87.51' // Replace with your Nginx server IP or hostname
        NGINX_USER = 'ubuntu' // Nginx server user with write permissions
        NGINX_HTML_PATH = '/var/www/html/' // Path where Nginx serves static content
        GIT_REPO_URL = 'https://github.com/Himanshu-0711/index-repo/' // GitHub repo URL
        GIT_BRANCH = 'main' // Branch from which to deploy
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Clean workspace and checkout code from GitHub
                cleanWs()
                git branch: "${GIT_BRANCH}", url: "${GIT_REPO_URL}"
            }
        }
        
        stage('Build') {
            steps {
                // If any build steps are needed, add them here
                // This stage might be used for static site generators like Jekyll, Hugo, etc.
                // Example: npm install, yarn build, etc.
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
                // Perform any post-deployment actions if needed
                // Example: Clear cache, reload Nginx configuration, etc.
                script {
                    // Reload Nginx to apply changes
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
