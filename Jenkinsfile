pipeline {
  agent {
    kubernetes {
        containerTemplate {
        name 'manifest-test'
        image 'garethr/kubeval:latest'
        ttyEnabled true
        command 'cat'
        }
    }
  }
  

  stages {         
    stage('Cloning Git') {
      steps {
          container('manifest-test'){
                git url: 'https://github.com/Apachy999/test_kube_manifest.git'
         
          }
      }
    }   
    
    stage('check') {
      steps {
          container('manifest-test'){
            sh """#!/bin/sh 
            
              kubeval --openshift fixtures/*
              
            """  
              
            
          }
      }
    }
      
  }
  
  post ('Notification') {
            success {
                slackSend (color: '#00FF00', message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})  " )
              //  slackUploadFile channel: "#apachy999-", filePath: "kubeval_list.txt"
               
            }
            failure {
                slackSend (color: '#FF0000', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL}) ")
            }           
    }  
  
}
