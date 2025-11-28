pipeline {
    agent any

    environment {
        GITHUB_TOKEN = credentials('github-token') // Ici, tu crées un secret Jenkins avec ton token
        REPO_URL = "https://github.com/joanloule5/portfolio.git"
        BRANCH = "main"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    git config user.email "joanloule5@gmail.com"
                    git config user.name "joanloule5"
                    git add .
                    git commit -m "Auto-deploy by Jenkins" || echo "Rien à commit"
                    git push https://${GITHUB_TOKEN}@github.com/joanloule5/portfolio.git main
                '''
            }
        }
    }

    post {
        success { echo "Déploiement terminé ✅" }
        failure { echo "Échec du déploiement ❌" }
    }
}
