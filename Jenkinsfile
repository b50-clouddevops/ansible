pipeline {
    agent any    
    environment {
        ENV_URL       = "pipeline.google.com"
        SSH_CRED      = credentials('SSH')
    }

    stages {

        stage('Perform Lint Checks') {    // Runs only when it's a feature branch 
            steps {
                sh "env"
                sh "echo Performing Link Checks"           
            }
        }

        stage('Do a Dry-Run') {            // Runs only when it's a PR 
            steps {
                sh "env"
                sh "ansible-playbook robot-dryrun.yml -e COMPONENT=mongodb -e ENV=dev -e ansible_user=${SSH_CRED_USR} -e ansible_password=${SSH_CRED_PSW}"           
            }
        }

        stage('Main') {            // Runs only when it's a PR 
            steps {
                sh "env"
                sh "echo"           
            }
        }

    }
}

// SSH_CRED_USR
// SSH_CRED_PSW