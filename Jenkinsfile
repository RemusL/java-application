pipeline {
    agent any

    stages {
        stage("Deploy") {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'webUser', keyFileVariable: 'identity', usernameVariable: 'userName')]) {
                    script {
                        def remote = [:]
                        remote.name = "web"
                        remote.host = "ec2-52-29-123-31.eu-central-1.compute.amazonaws.com"
                        remote.allowAnyHosts = true
                        remote.user = userName
                        remote.identityFile = identity
                        
//                      This command fails when trying to ssh to Ubuntu 22 with an com.jcraft.jsch.JSchException: Auth fail
//                      The reason is that JSch is outdated and is not working with rsa-sha2 required by the server.
//                      https://stackoverflow.com/questions/73135640/jschexception-auth-fail-on-ubuntu-22-04
//                      Solution is to allow sha-rsa by adding PubkeyAcceptedAlgorithms=+ssh-rsa into /etc/ssh/sshd_config on the server.
//                      Or use a previous version of Ubuntu that accepts sha-rsa.
                        sshCommand remote: remote, command: 'sudo docker run -t public.ecr.aws/l9o2c9u6/helloworld:1.0'
                    }
                }
            }
        }
    }
}
