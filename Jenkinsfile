pipeline {
  agent any
  tools{
    gradle 'gradle7.0'
  }
  // environment{
  //   SERVER_CREDENTIALS= credentials('')
  // }
  
  stages {
    stage('Build') {
      steps {
        echo 'Building'
        sh 'gradle build'
        sh 'npm install'
        // nodejs('node18.0.0'){
        //   sh 'npm install'
        // }
        
      }
    }
    stage('Test') {
      // when{
      //   expression{
      //     BRANCH_NAME=='test' || BRANCH_NAME=='master'
      //   }
      // }
      steps {
        echo 'Testing'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying'
        nodejs('node18.0.0'){
          sh 'node server'
        }
        // withCredentials{[
        //   usernamePassword(credentials:'credentials=id', usernameVariable:USER, passwordVariable:PWD)
        // ]}{
        //   sh "some script ${USER}  ${PWD}"
        // }
        //sh npm Build
      }
    }
    
  }
  post{
    always{
      echo 'Pipeline has executed'
    }
    success{
      echo 'Pipeline has been succeeded'
    }
    failure{
      echo 'Pipeline has failed'
    }
  }
}
