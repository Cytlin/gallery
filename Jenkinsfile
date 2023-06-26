pipeline {
  agent{
    node {
      label 'node18.0.0'
    }
  }  
  tools{
    gradle 'gradle7.0'
  }
  environment{
    BUILD_ID="${env.BUILD_ID}"
    RENDER_URL= 'https://cytlin-ip-1.onrender.com'
  }
  
  stages {
    stage('Build') {
      steps {
        echo 'Building'
        slackSend(message:"Build ID: ${env.BUILD_ID}  Render URL: ${env.RENDER_URL}")
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
        slackSend(message:"Build ID: ${env.BUILD_ID}  Render URL: ${env.RENDER_URL}")
        withCredentials([usernameColonPassword(credentialsId: 'render', variable: 'RENDER_CREDENTIALS' )]){
         sh 'git push https://${RENDER_CREDENTIALS}@git.render.com/mighty-earth-27385.git master'
         sh 'node server'
        }
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
                if (testResult != 1) {
                    slackSend(message:"Build ID: ${env.BUILD_ID}  Render URL: https://cytlin-ip-1.onrender.com ")
                }
            }

        }
 }
}
