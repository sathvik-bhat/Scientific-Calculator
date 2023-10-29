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
                git url: 'https://github.com/sathvik-bhat/Scientific-Calculator.git', branch: 'master',
                credentialsId: 'Credential_Git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                // sh 'tar czf Node.tar.gz node_modules src jenkins Jenkinsfile package.json public'
                sh 'tar czf node_modules src jenkins Jenkinsfile package.json public'
            }
        }
        
        // stage('Test') {
        //     steps {
        //         sh 'chmod +x ./jenkins/scripts/test.sh'
        //         sh './jenkins/scripts/test.sh'
        //     }
        // }
        // stage('Build Docker Image') {

        //     steps {
        //         script{
        //             // docker = sh '/usr/local/bin/docker'
        //             // dockerimage = docker.build registry + ":latest"
        //             dockerimage = sh 'docker build -t '+registry+':latest .'
        //             // dockerimage = sh '/var/lib/docker build -t '+registry+':latest .'
        //         }
        //     }
        // }
        // stage('Push Image to dockerHub') {
        //     steps {
        //         // script{
        //         //     // sh 'docker login -u "sathvik04" -p "$sibpwd123"'
        //         //     sh 'echo $DOCKERHUB_CRED'
        //         //     sh 'docker login -u "sathvik04" -p $DOCKERHUB_CRED'
        //         //     sh 'docker push ' +registry +':latest'
        //         // }

        //         withCredentials([string(credentialsId: 'dockerhub_pwd', variable: 'dockerhub_pwd')]) {
        //             sh 'docker login -u "sathvik04" -p ${dockerhub_pwd}'
        //             sh 'docker push ' +registry +':latest'
        //         }
        //         // withDockerRegistry([credentialsId: 'CRED_DOCKER', url: '']){
        //         //     sh '/usr/local/bin/docker push gaparul/calculator-react:latest'
        //         // }
        //         // sh 'echo $DOCKERHUB_CRED_PSW | /usr/local/bin/docker login -u $DOCKERHUB_CRED_USR --password-stdin'
                
                
        //     }
        // }
        // stage('Free local space') {
        //     steps {
        //         sh 'docker rmi $registry:latest'
        //     }
        // }

        stage('Deploy') {
            steps {
                // sh '/home/sathvik/.local/bin/ansible-playbook playbook.yml -i inventory -e image_name=sathvik04/scientific-calculator'
                ansiblePlaybook becomeUser: null, colorized: true, disableHostKeyChecking: true, installation: 'ansible', inventory: 'inventory',
                playbook: 'playbook.yml', sudoUser: null, extras: '-e "image_name=sathvik04/scientific-calculator"'
            }
        }
    }
}  