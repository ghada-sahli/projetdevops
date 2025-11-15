pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK'
    }

    stages {
        stage('Checkout') {
            steps {
                echo '========== Récupération du code source =========='
                checkout scm
            }
        }

        stage('Compilation') {
            steps {
                echo '========== Compilation du projet =========='
                sh 'mvn clean compile'
            }
        }

        stage('Tests Unitaires') {
            steps {
                echo '========== Exécution des tests unitaires =========='
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo '========== Création du package (JAR/WAR) =========='
                sh 'mvn package -DskipTests'
            }
        }
    }

    post {
        success {
            echo '✅ Build réussi !'
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
        failure {
            echo '❌ Build échoué !'
        }
        always {
            echo '🧹 Nettoyage terminé'
        }
    }
}