def remote = [:]
remote.name = "web"
remote.host = "52.29.123.31"
remote.allowAnyHosts = true

pipeline {
    agent any

    stages {
        stage('Build') {
//             steps {
//                 withMaven(maven : 'apache-maven-3.8.6') {
//                                 sh 'mvn clean install'
//                  }
//             }
        }

        stage('Run') {
//             steps {
//                 sh 'docker images'
//                 sh 'docker run -t helloworld:1.0'
//             }
        }
        stage("Deploy") {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'webUser', keyFileVariable: 'identity', usernameVariable: 'userName')]) {
                    remote.user = userName
                    remote.identityFile = identity
                    sshCommand remote: remote, command: 'pwd'
                }
            }
        }
    }
}
