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
                        sh 'sudo scp -o StrictHostKeyChecking=no -i ${privatekey} /var/lib/jenkins/workspace/Ansible_Jenkins/to_ansible/* root@${Ansible_server_IP}:/etc/ansible'
                    }
                }
            }
        }

        
        stage ("Executing the playbook on Ansible-server"){
            steps {
                script {
                    echo "calling ansible playbooks"
                    def remote = [:]
                    remote.name = 'test'
                    remote.host = ${Ansible_server_IP}
                    remote.user = 'root'
                    //remote.password = 'password'
                    remote.allowAnyHosts = true
                    withCredentials([string(credentialsId: 'path_to_Private_key', variable: 'privatekey', usernameVariable: 'root')]) {
                        remote.user = "root"
                        remote.identityFile = ${privatekey}
                        sshCommand remote: remote, command: "ls -lrt"
                        /*
                        sshScript remote: remote, script: "abc.sh"
                        sshPut remote: remote, from: 'abc.sh', into: '.
                        sshGet remote: remote, from: 'abc.sh', into: 'abc_get.sh', override: true
                        sshRemove remote: remote, path: "abc.sh"
                        */
                    }
                    
                }
            }
        }
        
    }
}