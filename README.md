pipeline {
    agent any
    
   environment {
        // Define environment variables if needed
        PATH = "${tool 'JDK-11'}/bin:${env.PATH}"
    }

  stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean install'  // Example command for a Maven project
            }
        }
        
  stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'  // Example command to run tests for a Maven project
            }
        }
        
  stage('Deploy') {
            steps {
                echo 'Deploying the project...'
                // Example deployment step (e.g., SCP, Docker, or cloud deployment)
                sh 'scp target/my-app.war user@server:/path/to/deploy'
            }
        }
    }
    
 post {
        success {
            echo 'Build and deployment were successful!'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}
