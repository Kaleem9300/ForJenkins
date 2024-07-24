pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/Kaleem9300/ForJenkins.git', branch: 'main')
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean compile'
      }
    }

    stage('Test') {
      steps {
        sh '''mvn test
'''
      }
    }

    stage('Post') {
      steps {
        junit(testResults: '**/target/surefire-reports/*.xml', allowEmptyResults: true)
      }
    }

  }
}