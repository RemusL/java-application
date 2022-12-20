pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                withMaven(maven : 'apache-maven-3.8.6') {
//                     sh 'mvn clean install'
                    sh 'echo Build'
                }
            }
        }

        stage('Run') {
            steps {
//                 sh 'docker images'
//                 sh 'docker run -t helloworld:1.0'
                sh 'echo Run'
            }
        }
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
                        sshCommand remote: remote, command: 'pwd'
                    }
                }
            }
        }
    }
}
