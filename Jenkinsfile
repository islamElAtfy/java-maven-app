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
                sh 'podman build -t lab-app:javamaven-3.9 .'
                }
        }
        stage('Deploy App') {
            steps {
                echo "Deploying the application..."
                sh 'sudo cp -r $(find /var/lib/jenkins/.local/share/containers/storage/overlay-images/ -type f -mmin -2) /var/lib/containers/storage/overlay-images' 
                sh 'podman run -d --name demo-java-application --restart=on-failure -v java-application:/var/java-application:Z -p 28888:28888 localhost/lab-app:javamaven-3.9'
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
