pipeline{
    agent any
    stages{
        stage ("Coping the files to Ansible-server") {
            steps {
                script {
                    sshagent(['anisble-jenkins']) {
                        sh 'scp -o StrictHostKeyChecking=no D:\stuffs\DevOps Learning\Repos\Asible_Jenkins_CICD_integration\to_anisble\* ubuntu@ec2-13-235-19-64.ap-south-1.compute.amazonaws.com:/root'
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