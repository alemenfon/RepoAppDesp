pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    docker.image('maven:3.9.0').inside {
                        sh 'mvn -B -DskipTests clean package'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image('maven:3.9.0').inside {
                        sh 'mvn test'
                    }
                }
                post {
                    always {
                        junit 'target/surefire-reports/*.xml'
                    }
                }
            }
        }
        stage('Deliver') {
            steps {
                script {
                    docker.image('maven:3.9.0').inside {
                        sh './jenkins/scripts/deliver.sh'
                    }
                }
            }
        }
    }
}

