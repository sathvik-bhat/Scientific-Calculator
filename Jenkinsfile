pipeline {
    
    agent {
        any {
            label 'docker'
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
    
    // tools {nodejs "nodejs"}
     environment {
            CI = 'true'
            registry = 'sathvik04/scientific-calculator'
            DOCKERHUB_CRED = credentials('dockerhub_id')
            registryCredential = 'dockerhub_id'
            dockerimage = ''
      }
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
        stage('Build Docker Image') {

            steps {
                script{
                    // docker = sh '/usr/local/bin/docker'
                    // dockerimage = docker.build registry + ":latest"
                    dockerimage = sh 'docker build -t '+registry+':latest .'
                    // dockerimage = sh '/var/lib/docker build -t '+registry+':latest .'
                }
            }
        }
    }
}