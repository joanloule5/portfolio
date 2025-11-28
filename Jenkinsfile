stage('Deploy to Windows') {
    steps {
        echo "Déploiement local Windows"
        withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
            bat '''
            cd C:\\deploy-site\\site
            git config --global user.email "joanloule5@gmail.com"
            git config --global user.name "joanloule5"

            git add .
            git commit -m "Auto-deploy by Jenkins" || echo "Rien à commit"

            git push https://%GITHUB_TOKEN%@github.com/joanloule5/portfolio.git main
            '''
        }
    }
}
