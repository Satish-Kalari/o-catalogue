pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    } 

    // Just like variables 
    environment {
        packageVersion = ''       
    }
    
    // Terminating Build if it takes certain time
     options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds() 
    }
        
    // BUILD
    stages {
        stage('getting version no') {
            steps {
                script {
                    def packageVersion = readJSON file: 'package.json'
                    packageVersion = packgaeJson.version
                    echo "application version: $packageVersion"
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }        
    }

    // POST BUILD
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
         failure { 
            echo 'This runs when pipeline is failed, used set alert'
        }
         success { 
            echo 'This runs when pipeline is SUCCESS'
        }
    }
}