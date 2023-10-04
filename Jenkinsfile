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
                    withCredentials([string(credentialsId: 'path_to_Private_key', variable: 'privatekey')]) {
                        sh 'sudo scp -o StrictHostKeyChecking=no -i ${privatekey} /var/lib/jenkins/workspace/Jenkins_ansible_CiCD/to_ansible/* ubuntu@ec2-35-154-71-112.ap-south-1.compute.amazonaws.com:/etc/ansible'
                    }
                }
            }
        }

        /*
        stage ("Executing the playbook on Ansible-server"){
            steps {
                script {
                    withCredentials([string(credentialsId: 'path_to_Private_key', variable: 'privatekey')]) {
                        sh 'sudo ssh -i ${privatekey} ubuntu@ec2-35-154-71-112.ap-south-1.compute.amazonaws.com "ansible-playbook /jenkins/"'
                    }
                }
            }
        }
        */
    }
}