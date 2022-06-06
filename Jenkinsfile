pipeline {
  agent any

  environment {
    FIREBASE_TOKEN_CREDENTIALS_ID = 'firebase_token_credentials_id'
  }

  stages {
    stage('Unit Test') {
        steps {
            sh 'cp /home/ubuntu-22-04/local.properties local.properties'
            sh './gradlew clean testDebugUnitTest'
        }
    }

    stage('Distribute App to Firebase') {
        steps {
            withCredentials([string(credentialsId: "$FIREBASE_TOKEN_CREDENTIALS_ID", variable: 'FIREBASE_TOKEN')]) {
                sh "export FIREBASE_TOKEN=$FIREBASE_TOKEN"
                sh 'fastlane android distribute'
            }
        }
    }
  }
}
