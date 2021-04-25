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
              git 'https://github.com/Apachy999/test_kube_manifest.git'
          }
      }
    }   
    
    
               class FileExample {
                 static void main(String[] args) {
                   new File("fixtures").eachFileMatch(~/.*.txt/) { file ->
                      println file.getName()   
    
    stage('check') {
      steps {
          container('manifest-test'){
            sh """#!/bin/sh 
            
              kubeval --openshift fixtures/*
              
              

      }
   }

              
            """  
              
            
          }
      }
    }
      
 
  }
}
