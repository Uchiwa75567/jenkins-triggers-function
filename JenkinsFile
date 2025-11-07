pipeline {
    agent any

    triggers {
        // 1️⃣ Détecte les changements dans le dépôt toutes les 5 minutes
        pollSCM('H/5 * * * *')

        // 2️⃣ Déclenchement planifié toutes les 10 minutes
        cron('H/10 * * * *')

        // 3️⃣ Déclenchement après un autre job Jenkins
        upstream(upstreamProjects: 'JobPrincipal', threshold: hudson.model.Result.SUCCESS)
    }

    parameters {
        string(name: 'MESSAGE', defaultValue: 'Build simple project', description: 'Message à afficher')
    }

    stages {
        stage('Préparation') {
            steps {
                echo "✅ Début du build : ${params.MESSAGE}"
            }
        }

        stage('Exécution script') {
            steps {
                sh './script.sh'
            }
        }
    }

    post {
        success {
            echo "✅ Build terminé avec succès à ${new Date()}"
        }
        failure {
            echo "❌ Build échoué à ${new Date()}"
        }
    }
}
