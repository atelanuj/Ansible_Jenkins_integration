pipeline{
    agent any
    stages{
        stage ("Git Checkout") {
            steps {
                script {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/atelanuj/Ansible_Jenkins_integration.git']])
                }
            }
        }

        stage ("Coping the files to Ansible-server") {
            steps {
                script {
                    sshagent(['anuj.pem']) {
                        sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/Jenkins_ansible_CiCD/to_ansible/* root@ec2-35-154-71-112.ap-south-1.compute.amazonaws.com:/jenkins'
                    }
                }
            }
        }

        /*
        stage ("Executing the playbook on Ansible-server"){
            steps {
                script {
                    
                }
            }
        }
        */
    }
}