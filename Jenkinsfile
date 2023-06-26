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
}
}
