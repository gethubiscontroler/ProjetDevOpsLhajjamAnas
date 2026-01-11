pipeline {
    agent any

    tools {
        maven 'maven' 
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn -B clean package -f myapp/pom.xml'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'myapp/target/*.jar', fingerprint: true
            }
        }
    }

    // Ajout de la section de notification Slack
    post {
        success {
            slackSend (
                channel: '#tous-projetdevopslhajjamanas', 
                color: 'good', 
                message: "✅ Build Réussi : Le projet ${env.JOB_NAME} (n°${env.BUILD_NUMBER}) est prêt. Artifact archivé."
            )
        }
        failure {
            slackSend (
                channel: '#tous-projetdevopslhajjamanas', 
                color: 'danger', 
                message: "❌ Build Échoué : Une erreur est survenue sur ${env.JOB_NAME} (n°${env.BUILD_NUMBER})."
            )
        }
    }
}