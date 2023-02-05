pipeline {
     agent any
        
     stages {
         stage('Checkout') {
             steps {
                 git branch: 'main', url: 'https://github.com/patangana/jenkins-terraform-aws.git'
             }
         }
         stage('Checkov') {
             steps {
                 script {
                     docker.image('bridgecrew/checkov:latest').inside("--entrypoint=''") {
                         try {
                             sh 'checkov -d . --use-enforcement-rules -o cli -o junitxml --output-file-path console,results.xml --repo-id utrains/jenkins-terraform-aws --branch main --bc-api-key 81765d74-7448-419d-b97e-758078a64b7c'
                             junit skipPublishingChecks: true, testResults: 'results.xml'
                         } catch (err) {
                             junit skipPublishingChecks: true, testResults: 'results.xml'
                             throw err
                         }
                     }
                 }
             }
         }
     }
     options {
         preserveStashes()
         timestamps()
     }
 }