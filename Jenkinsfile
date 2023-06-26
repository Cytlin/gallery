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
  MY_VARIABLE = 'my value'
  
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
}
