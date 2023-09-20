pipeline {
    agent any
    tools {
        maven 'maven-3.9'
    }
    stages {
        stage('Build Jar') {
            steps {
                echo "Building the application..."
                sh 'mvn package'
            }
        }
        stage('Build Podman Image') {
            steps {
                echo "Building the Podman image..."
                sh 'sudo podman build -t lab-app:javamaven-3.9 .'
                sh 'sudo podman images'
                sh 'sudo whoami'
                }
        }
    }
    post {
        success {
            echo "Success! The pipeline has completed successfully."
            // You can add further actions or notifications on success here
        }
        failure {
            echo "Pipeline failed. Please investigate and take necessary actions."
            // You can add further actions or notifications on failure here
        }
    }
}
