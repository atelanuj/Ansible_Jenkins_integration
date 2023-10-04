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
                        sh 'sudo scp -o StrictHostKeyChecking=no -i ${privatekey} /var/lib/jenkins/workspace/Jenkins_ansible_CiCD/to_ansible/* root@13.127.215.48:/etc/ansible'
                    }
                }
            }
        }

        
        stage ("Executing the playbook on Ansible-server"){
            steps {
                script {
                    echo "calling ansible playbooks"
                    def remote = [:]
                    remote.name = "ansible-server"
                    remote.hosts = "13.127.215.48"
                    remote.allowAnyHosts = true
                    withCredentials([string(credentialsId: 'path_to_Private_key', variable: 'privatekey')]) {
                        remote.user = root 
                        remote.identityfile =  privatekey 
                        sshcommand remote: remote, command: "ls -l"
                    }
                    
                }
            }
        }
        
    }
}