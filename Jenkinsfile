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
        sh 'gradle build'
        sh 'npm install'       
      }
    }
    stage('Test') {
      steps {
        echo 'Testing'
        script{
          def npmTestOutput= sh(returnStdout: true, script: 'npm test')
          //check if test fails
          if(npmTestOutput.contains('fail')){
            emailext(
              subject:'Test Results - Failed',
              body: 'The tests have failed. Please investigate.',
              to: 'cytlinadhiambo@gmail.com'
            )
          }

        }
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying'
        withCredentials([usernameColonPassword(credentialsId: 'render', variable: 'RENDER_CREDENTIALS' )]){
         sh 'git push https://${RENDER_CREDENTIALS}@git.render.com/mighty-earth-27385.git master'
         sh 'node server'
        }
      }    
    }  
  }
  post {
  //if deploy is successful
        success {      
            slackSend(message:"Build ID: ${env.BUILD_ID}  Render URL: ${env.RENDER_URL}")
        }
  }
}
