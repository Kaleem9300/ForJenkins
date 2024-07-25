pipeline {
  agent any
  tools {
        // Define Maven tool
        maven 'MAVAN_HOME'
    }

    environment {
        // Define environment variables if needed
        MAVEN_OPTS = '-Xmx2g'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from Git
                git url: 'https://github.com/Kaleem9300/ForJenkins.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Run Maven clean and compile
                script {
                    def mvnHome = tool 'MAVAN_HOME'
                    bat "\"${mvnHome}\\bin\\mvn\" clean compile"
                }
            }
        }

        stage('Test') {
            steps {
                // Run Maven tests using TestNG
                script {
                    def mvnHome = tool 'MAVAN_HOME'
                    bat "\"${mvnHome}\\bin\\mvn\" test"
                }
            }
            post {
                always {
                    // Archive TestNG test results
                    junit '**/target/surefire-reports/*.xml'  // Adjust path as necessary
                }
            }
        }

        stage('Package') {
            steps {
                // Package the application
                script {
                    def mvnHome = tool 'MAVAN_HOME'
                    bat "\"${mvnHome}\\bin\\mvn\" package"
                }
            }
        }

        stage('Archive') {
            steps {
                // Archive build artifacts
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            // Perform actions regardless of build status
            echo 'Cleaning workspace...'
            cleanWs()
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed.'
        }
        unstable {
            echo 'Build is unstable.'
        }
    }
}
