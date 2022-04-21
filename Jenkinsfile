pipeline {
    agent {
        label 'Mac_Mini'
    }

    

    stages {
        

        stage('Checkout code') {
            steps {
                 script {

  def scmVars = checkout scm
  echo 'scm : the commit id is ' +scmVars.GIT_COMMIT
  echo 'scm : the commit branch  is ' +scmVars.GIT_BRANCH
  echo 'scm : the previous commit id is ' +scmVars.GIT_PREVIOUS_COMMIT
                     
 def lastCommiterEmail = sh(returnStdout: true, script: 'git log --format="%ae" | head -1').trim()
                     echo 'last commit email is'  +lastCommiterEmail.GIT_AUTHOR


   }
  }
}
        
        
    
        
        
        stage('Build star Notify') {
            steps {
             slackSend channel: 'chopt-chatops', iconEmoji: '', color: "#439FE0", message: "chopt_ios:   Build Started - ${env.BRANCH_NAME} ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", teamDomain: 'ymedialabs', tokenCredentialId: 'chopt-chatops-id', username: 'jenkins'
                   }   
                }
                
        stage(Hello) {
            steps {
                sh "echo Hello"
                           
            }
        }
    }
    post {
        success {
        slackSend channel: 'chopt-chatops', color: 'good', iconEmoji: '', message: "chopt_ios:   Build deployed successfully - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", teamDomain: 'ymedialabs', tokenCredentialId: 'chopt-chatops-id', username: 'jenkins'
        }  
         
         
        failure {
        slackSend failOnError: 'true', channel: 'chopt-chatops', color: 'danger', iconEmoji: '', message: "chopt_ios:   Build failed  - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", teamDomain: 'ymedialabs', tokenCredentialId: 'chopt-chatops-id', username: 'jenkins'
        } 
         
        unstable {
        slackSend channel: 'chopt-chatops', iconEmoji: '', color: 'warning',  message: "chopt_ios:   Build unstable - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", teamDomain: 'ymedialabs', tokenCredentialId: 'chopt-chatops-id', username: 'jenkins'                    
        }
        
        aborted {
        slackSend channel: 'chopt-chatops', iconEmoji: '', color: 'warning',  message: "chopt_ios:   Build aborted - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", teamDomain: 'ymedialabs', tokenCredentialId: 'chopt-chatops-id', username: 'jenkins'                    
        }

        cleanup {
            cleanWs deleteDirs: true, notFailBuild: true, patterns: [[pattern: '', type: 'INCLUDE']]
         }
    }
}


