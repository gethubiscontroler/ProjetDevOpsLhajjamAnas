pipeline {
    agent any

    tools {
        // Assurez-vous que Maven est configuré dans "Global Tool Configuration" sur Jenkins avec ce nom
        maven 'maven' 
    }

    stages {
        stage('Checkout SCM') {
            steps {
                // Récupération du code depuis votre dépôt GitHub
                checkout scm
            }
        }

        stage('Build Maven') {
            steps {
                // Exécution de la compilation. Le flag -f pointe vers votre dossier myapp
                sh 'mvn -B clean package -f myapp/pom.xml'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Sauvegarde du fichier .jar généré
                archiveArtifacts artifacts: 'myapp/target/*.jar', fingerprint: true
            }
        }
    }
}