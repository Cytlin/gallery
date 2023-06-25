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
        sh 'node server'
      }
    }
    
  }

  post {
        always {
            // Send email notification only if tests fail
            script {
                def testResult = sh(returnStatus: true, script: 'npm test')
                if (testResult != 0) {
                    emailext subject: 'Test Results - Failed',
                        body: 'The tests have failed. Please investigate.',
                        to: 'cytlinadhiambo@gmail.com'
                }
            }

            script {
                def deployResult = sh(returnStatus: true, script: 'node server')
                if (deployResult = 0) {
                    slackSend(message:"Build ID: ${env.BUILD_ID}  Render URL: ")
                }
            }
        }
  }
}

