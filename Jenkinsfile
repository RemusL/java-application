pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                withMaven(maven : 'apache-maven-3.8.6') {
                                sh 'mvn clean install'
                 }
            }
        }

        stage('Run') {
            steps {
                sh 'docker images'
                sh 'docker run -t helloworld:1.0'
            }
        }
    }
}
