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
                    sshagent(['anisble-jenkins']) {
                        sh 'scp -o StrictHostKeyChecking=no $JENKINS_HOME/Jenkins_ansible_CiCD/to_ansible/* ubuntu@ec2-13-235-19-64.ap-south-1.compute.amazonaws.com:/root'
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