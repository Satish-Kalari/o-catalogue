pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    } 

    // Just like variables 
    environment {
        packageVersion = ''
        // nexusURL = '<place nexsus ec2 instance public ip adddress here>:8081'        
    }
    
    // Terminating Build if it takes certain time
     options {
        ansiColor("xterm")
        timeout(time: 1, unit: 'HOURS')
        // dose not allow two pipleline builds at a time 
        disableConcurrentBuilds() 
    }
      
    // BUILD
    stages {
        stage('Getting Package Ver No') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    packageVersion = packageJson.version 
                    echo "Aplication Ver No: $packageVersion"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh """
                    npm install
                """
            }
        }
        
         stage('Build') {
            steps {
                sh """
                    ls -la
                    zip -q -r catalogue.zip ./* -x ".git" -x "*.zip"
                    ls -ltr
                """
            }
        }
        // stage('Publish Artifact') {
        //     steps {
        //          nexusArtifactUploader(
        //             nexusVersion: 'nexus3',
        //             protocol: 'http',
        //             nexusUrl: "${nexusURL}",
        //             groupId: 'com.roboshop',
        //             version: "${packageVersion}",
        //             repository: 'catalogue',
        //             credentialsId: 'nexus-auth',
        //             artifacts: [
        //                 [artifactId: 'catalogue',
        //                 classifier: '',
        //                 file: 'catalogue.zip',
        //                 type: 'zip']
        //             ]
        //         )
        //     }
        // }
        // stage('Deploy') {
        //     steps {
        //         script {
        //                 def params = [
        //                     string(name: 'version', value: "$packageVersion"),
        //                     string(name: 'environment', value: "dev")
        //                 ]
        //                 build job: "catalogue-deploy", wait: true, parameters: params
        //             }
        //     }
        // }
              
    }

    // POST BUILD
    post { 
        always { 
            echo 'I will always say Hello again!'
            // This will remove pipleline log files
            deleteDir() 
        }
         failure { 
            echo 'This runs when pipeline is failed, used set alert'
        }
         success { 
            echo 'This runs when pipeline is SUCCESS'
        }
    }
}