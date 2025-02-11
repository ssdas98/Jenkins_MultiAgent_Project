pipeline {
    agent none
        environment {
            NGINX_HTML_DIR = "/usr/share/nginx/html"
			REPO_URL = 'https://github.com/ssdas98/Jenkins_MultiAgent_Project.git'
			BRANCH = 'main'
        }
        stages {
            stage('Clone Repository') {
                agent { label 'Slavenode1' }
                steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
                }
            }
            stage('Run Shell Script') {
                agent { label 'Slavenode1' }
                steps {
                    script {
                        sh 'chmod 777 Hello.sh'
                        sh './Hello.sh'
                    }
                }
            }
            stage('Install nginx') {
                agent { label 'Slavenode2' }
                steps {
                    script {
                        sh 'sudo apt-get update -y'
                        sh 'sudo apt-get install nginx -y'
                    }
                }
            }
            stage('Configure nginx') {
                agent { label 'Slavenode2' }
                steps {
                    script {
                        sh 'echo "<html><body><h1>Welcome to Jenkins Nginx Deployment!</h1></body></html>" > sudo tee ${NGINX_HTML_DIR}/index.html > /dev/null'
                        sh 'sudo nginx -t'
                    }
                }
            }
            stage('Start nginx') {
                agent { label 'Slavenode2' }
                steps {
                    script {
                        sh 'sudo systemctl start nginx'
                        sh 'sudo systemctl enable nginx'
                    }
                }
            }
            stage('Verify nginx') {
                agent { label 'Slavenode2' }
                steps {
                    script {
                        sh 'sudo systemctl status nginx'
                    }
                }
            }
        }
        post {
            success {
                echo 'nginx installed successfully!'
            }
            failure {
                echo 'nginx installation failed!'
            }
        }
}
