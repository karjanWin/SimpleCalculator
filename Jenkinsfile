pipeline {
    agent any

    tools {
        maven 'Maven-BT' // Make sure Maven is installed and configured in Jenkins
    }

   stages {
        stage('Checkout') {
            steps {
                // Use the credentialsId to authenticate to the GitHub repository
                git url: 'https://github.com/karjanWin/SimpleCalculator.git',
                    branch: 'master',
                    credentialsId: 'github-pat'  // Use the ID you set earliero URL
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
