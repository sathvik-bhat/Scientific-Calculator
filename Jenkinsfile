pipeline {
    
    agent {
        any {
            label 'docker'
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
    
    // tools {nodejs "nodejs"}
    //  environment {
    //         CI = 'true'
    //         registry = 'gaparul/scientific-calculator-react'
    //         DOCKERHUB_CRED = credentials('CRED_DOCKER')
    //         registryCredential = 'CRED_DOCKER'
    //         dockerimage = ''
    //   }
    stages {
        stage('Git Pull') {
            steps {
                git url: 'https://github.com/gaparul/Scientific-Calculator.git', branch: 'master',
                credentialsId: 'Credential_Git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'tar czf Node.tar.gz node_modules src jenkins Jenkinsfile package.json public'
            }
        }
        stage('Test') {
            steps {
                sh 'chmod +x ./jenkins/scripts/test.sh'
                sh './jenkins/scripts/test.sh'
            }
        }
        //
    }
}