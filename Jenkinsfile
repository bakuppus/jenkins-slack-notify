pipeline {
    agent {
        label 'Mac_Mini'
    }

    stages {
        
        stage ('Checkout') {

        scmInfo = checkout scm

        /*...*/
        echo "scm : ${scmInfo}"
        echo "${scmInfo.GIT_COMMIT}"
    }
        
        stage('Build star Notify') {
            steps {
             slackSend channel: 'chopt-chatops', iconEmoji: '', color: "#439FE0", message: "chopt_ios:   Build Started - ${env.BRANCH_NAME} ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", teamDomain: 'ymedialabs', tokenCredentialId: 'chopt-chatops-id', username: 'jenkins'
                   }   
                }
                
        stage(Hello) {
            steps {
                sh "echo Hello"
                echo $GIT_BRANCH
                echo $GIT_URL
                            
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

