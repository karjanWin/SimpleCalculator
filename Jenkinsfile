pipeline {
    agent any

    tools {
        maven 'Maven-BT' // Make sure Maven is installed and configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/karjanWin/SimpleCalculator.git' // Update with your repo URL
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package' // Clean and package your application
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test' // Run unit tests
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') { // 'SonarQube' is the name you configured earlier
                    sh 'mvn sonar:sonar' // Execute SonarQube analysis
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment stage...' // Placeholder for deployment steps (optional)
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml' // Publish test results
        }
    }
}
