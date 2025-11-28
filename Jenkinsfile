pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy to Windows') {
            steps {
                echo "Déploiement local Windows"
                bat '''
                cd C:\\deploy-site\\site
                git pull
                '''
            }
        }
    }

    post {
        success {
            echo 'Déploiement réussi !'
        }
    }
}

