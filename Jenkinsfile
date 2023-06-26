pipeline {
  agent any
  tools{
    gradle 'gradle7.0'
  }
  environment{
    BUILD_ID="${env.BUILD_ID}"
  }
  
  stages {
    stage('Build') {
      steps {
        echo 'Building'
        slackSend(message:"Build ID: ${env.BUILD_ID}  Render URL: ")
        sh 'gradle build'
        sh 'npm install'       
      }
    }
    stage('Test') {
      steps {
        echo 'Testing'
        sh 'npm test'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying'
        slackSend(message:"Build ID: ${env.BUILD_ID}  Render URL: ")
        withCredentials([usernameColonPassword(credentialsId: 'heroku', variable: 'HEROKU_CREDENTIALS' )]){
         sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/mighty-earth-27385.git master'
         sh 'node server'
        }
    }
    
  }

  // post {
  //       always {
  //           // Send email notification only if tests fail
  //           script {
  //               def testResult = sh(returnStatus: true, script: 'npm test')
  //               if (testResult != 0) {
  //                   emailext subject: 'Test Results - Failed',
  //                       body: 'The tests have failed. Please investigate.',
  //                       to: 'cytlinadhiambo@gmail.com'
  //               }
  //           }

  //           script {
  //               def deployResult = sh(returnStatus: true, script: 'node server')
  //               if (testResult != 0) {
  //                   slackSend(message:"Build ID: ${env.BUILD_ID}  Render URL: ")
  //               }
  //           }

  //       }
  // }
}
}
