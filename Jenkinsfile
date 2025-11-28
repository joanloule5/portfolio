pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validation') {
            steps {
                bat 'echo Validation HTML/CSS (aucun build nécessaire)'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/*.html, **/*.css, **/*.js, **/assets/**', fingerprint: true
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
                    bat """
                    cd C:\\deploy-site\\site

                    git config --global user.email "joanloule5@gmail.com"
                    git config --global user.name "joanloule5"

                    git add .
                    git commit -m "Auto-deploy by Jenkins" || echo Rien à commit

                    git push https://%GITHUB_TOKEN%@github.com/joanloule5/portfolio.git main
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Déploiement réussi !'
        }
        failure {
            echo 'Échec du déploiement'
        }
    }
}
