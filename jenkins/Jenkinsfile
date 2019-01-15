pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'pwd'
                sh 'mvn -B -DskipTests clean package'
                sh 'pwd'
            }
        }
        stage('Test') {
            steps {
                sh 'pwd'
                sh 'mvn test'
                sh 'pwd'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh 'pwd'
                sh './jenkins/scripts/deliver.sh'
                sh 'pwd'
            }
        }
    }
}
