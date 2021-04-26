pipeline {
    
 // triggers { 
   //     cron('H/10 * * * *')
//    }
    
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
    
    stage('Checking GIT manifests') {
      steps {
          container('manifest-test'){

             sh """#!/bin/sh 
             kubeval --openshift fixtures/* > kubeval_list.txt
           
            res="\$(sed '/^PASS/d'  kubeval_list.txt)"
            
            echo \$res
         
            """ 
            
          }
      }
    }
    

 
  }
  
  post ('Notification') {
           success {
              
                slackSend (color: '#00FF00', message: " kubeval_list.txt SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL}) " )
                
               
            }
            failure {
                slackSend (color: '#FF0000', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL}) ")
            }
            
    }  
  
}
