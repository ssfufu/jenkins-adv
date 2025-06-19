pipeline {
    agent {
        label 'agent-vm'
    }
    
    environment {
        IMAGE_NAME = 'mon-site-web'
        CONTAINER_NAME = 'mon-site-web-container'
        PORT = '8888'
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Construction de l\'image Docker...'
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Déploiement...'
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm ${CONTAINER_NAME} || true"
                sh "docker run -d --name ${CONTAINER_NAME} -p ${PORT}:80 ${IMAGE_NAME}"
            }
        }
    }
    
    post {
        success {
            echo "Site déployé avec succès sur http://localhost:${PORT}"
        }
    }
}
