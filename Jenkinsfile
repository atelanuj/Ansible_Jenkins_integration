pipeline{
    agent any
    parameters{
        string(name: 'Ansible_server_IP', description: "Enter the Server_IP", defaultValue: "None")
    }
    
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
                        sh 'sudo scp -o StrictHostKeyChecking=no -i ${privatekey} ${JENKINS_HOME}/Jenkins_ansible_CiCD/to_ansible/* root@${Ansible_server_IP}:/etc/ansible'
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
                    remote.hosts = ${Ansible_server_IP}
                    remote.allowAnyHosts = true
                    withCredentials([string(credentialsId: 'path_to_Private_key', variable: 'privatekey', usernameVariable: 'root')]) {
                        remote.user = root 
                        remote.identityfile =  privatekey 
                        sshcommand remote: remote, command: "ls -l /"
                    }
                    
                }
            }
        }
        
    }
}