pipeline {
    agent none
    stages {
        stage('Test curl') {
            agent {
                docker { 
                    image 'garethr/kubeval' 
                    args "--network=host"
                }
            }
            steps {
                sh """#!/bin/sh

                """
            }
        }
    }
}
