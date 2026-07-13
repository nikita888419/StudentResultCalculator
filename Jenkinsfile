pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Parallel Build') {
            parallel {

                stage('Unit Test') {
                    steps {
                        sh 'mvn test'
                    }
                }

                stage('Package') {
                    steps {
                        sh 'mvn package'
                    }
                }
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar'
        }
    }
}
