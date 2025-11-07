pipeline {
    agent any // Exécute la pipeline sur n'importe quel agent disponible

    triggers { // Bloc définissant les déclencheurs automatiques de la pipeline
        // 1️⃣ Détecte les changements dans le dépôt toutes les 5 minutes
        pollSCM('H/5 * * * *') // Vérifie le SCM toutes les 5 minutes et déclenche une build seulement s'il y a des changements

        // 2️⃣ Déclenchement planifié toutes les 10 minutes
        cron('H/10 * * * *') // Déclenche la build toutes les 10 minutes, indépendamment des changements dans le SCM

        // 3️⃣ Déclenchement après un autre job Jenkins
        upstream(upstreamProjects: 'JobPrincipal', threshold: hudson.model.Result.SUCCESS) // Lance cette pipeline si 'JobPrincipal' termine avec au moins SUCCESS
    }

    parameters { // Déclare les paramètres que l'utilisateur peut fournir lors du lancement
        string(name: 'MESSAGE', defaultValue: 'Build simple project', description: 'Message à afficher') // Paramètre string accessible via params.MESSAGE
    }

    stages { // Contient les différentes étapes (stages) de la pipeline
        stage('Préparation') { // Stage de préparation affiché dans l'UI
            steps { // Actions à exécuter dans ce stage
                echo "✅ Début du build : ${params.MESSAGE}" // Affiche le message fourni par le paramètre MESSAGE
            } // Fin du bloc steps pour 'Préparation'
        } // Fin du stage 'Préparation'

        stage('Exécution script') { // Stage pour lancer un script shell
            steps { // Actions du stage
                sh './script.sh' // Exécute le script script.sh dans le workspace (attention au code de sortie non nul)
            } // Fin du bloc steps pour 'Exécution script'
        } // Fin du stage 'Exécution script'
    } // Fin du bloc stages

    post { // Actions post-build selon le résultat
        success { // Si la build réussit
            echo "✅ Build terminé avec succès à ${new Date()}" // Affiche la date/heure de réussite
        } // Fin du bloc success
        failure { // Si la build échoue
            echo "❌ Build échoué à ${new Date()}" // Affiche la date/heure d'échec
        } // Fin du bloc failure
    } // Fin du bloc post
} // Fin du pipeline
