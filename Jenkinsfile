pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        // Unix/Linux : On utilise `make` via `sh`
                        sh 'make'
                    } else {
                        // Windows : On utilise `make` via `bat`
                        bat 'make'
                    }
                }
            }
        }

        stage('Permissions') {
            when {
                expression { isUnix() }  // Ce stage ne s'exécute que sur Unix/Linux
            }
            steps {
                script {
                    sh 'chmod +x StringInverser'
                }
            }
        }

        stage('Nettoyage') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'make clean'
                    } else {
                        bat 'make clean'
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ Build et nettoyage terminés avec succès !"
        }
        failure {
            echo "❌ Erreur lors de la compilation ou du nettoyage."
        }
    }
}
