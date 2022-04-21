pipeline {
    agent {
        label 'Mac_Mini'
    }

    

    stages {
        

        stage('GitInfo') {
            steps {
                 script {

  def scmVars = checkout scm
  echo 'scm : the commit id is ' +scmVars.GIT_COMMIT
  echo 'scm : the commit branch  is ' +scmVars.GIT_BRANCH
  echo 'scm : the previous commit id is ' +scmVars.GIT_PREVIOUS_COMMIT                                      
  def commitEmail = sh(returnStdout: true, script: 'git log --format="%ae" | head -1').trim()
  GIT_COMMITTER_EMAIL = "${commitEmail}"
  echo "the commiter email is '${GIT_COMMITTER_EMAIL}'"
  def commitName = sh(returnStdout: true, script: 'git log --format="%an" | head -1').trim()
  GIT_COMMITTER_NAME = "${commitName}"
  echo " the commiter name is'${GIT_COMMITTER_NAME}'"


   }
  }
}
        
        
    
        
        
        stage('Build star Notify') {
            steps {
             slackSend channel: 'chopt-chatops', iconEmoji: '', color: "#439FE0", message: "chopt_ios:   Build Started - Commiter: ${GIT_COMMITTER_NAME}  Branch: ${GIT_BRANCH} Job: ${env.JOB_NAME} Build No: ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>) ", teamDomain: 'ymedialabs', tokenCredentialId: 'chopt-chatops-id', username: 'jenkins'
                   }   
                }
                
        stage(Hello) {
            steps {
                sh "echo Hello"
                echo "${GIT_COMMIT}"
                echo "${GIT_BRANCH}"
                echo "${GIT_PREVIOUS_COMMIT}"
                echo "${GIT_COMMITTER_EMAIL}"
                echo "${GIT_COMMITTER_NAME}"

                           
            }
        }
    }
    post {
        success {
        slackSend channel: 'chopt-chatops', color: 'good', iconEmoji: '', message: "chopt_ios:   Build deployed successfully - Commiter: ${GIT_COMMITTER_NAME}  Branch: ${GIT_BRANCH} Job: ${env.JOB_NAME} Build No: ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>) ", teamDomain: 'ymedialabs', tokenCredentialId: 'chopt-chatops-id', username: 'jenkins'
        }  
         
         
        failure {
        slackSend failOnError: 'true', channel: 'chopt-chatops', color: 'danger', iconEmoji: '', message: "chopt_ios:   Build failed  - Commiter: ${GIT_COMMITTER_NAME}  Branch: ${GIT_BRANCH} Job: ${env.JOB_NAME} Build No: ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>) ", teamDomain: 'ymedialabs', tokenCredentialId: 'chopt-chatops-id', username: 'jenkins'
        } 
         
        unstable {
        slackSend channel: 'chopt-chatops', iconEmoji: '', color: 'warning',  message: "chopt_ios:   Build unstable - Commiter: ${GIT_COMMITTER_NAME}  Branch: ${GIT_BRANCH} Job: ${env.JOB_NAME} Build No: ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>) ", teamDomain: 'ymedialabs', tokenCredentialId: 'chopt-chatops-id', username: 'jenkins'                    
        }
        
        aborted {
        slackSend channel: 'chopt-chatops', iconEmoji: '', color: 'warning',  message: "chopt_ios:   Build aborted - Commiter: ${GIT_COMMITTER_NAME}  Branch: ${GIT_BRANCH} Job: ${env.JOB_NAME} Build No: ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>) ", teamDomain: 'ymedialabs', tokenCredentialId: 'chopt-chatops-id', username: 'jenkins'                    
        }

        cleanup {
            cleanWs deleteDirs: true, notFailBuild: true, patterns: [[pattern: '', type: 'INCLUDE']]
         }
    }
}


