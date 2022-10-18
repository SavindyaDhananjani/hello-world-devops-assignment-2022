pipeline {
    agent any
    stages {
        stage('git repo') {
            steps {
                bat "git clone https://github.com/SavindyaDhananjani/hello-world-devops-assignment-2022.git"
            }
        }
        stage('clean') {
                    steps {
                        bat "mvn clean -f hello-world-devops-assignment-2022"
                    }
                }
        stage('install') {
            steps {
                bat "mvn install -f hello-world-devops-assignment-2022"
            }
        }
        stage('test') {
            steps {
                bat "mvn test -f hello-world-devops-assignment-2022"
            }
        }
        stage('package') {
            steps {
                bat "mvn package -f hello-world-devops-assignment-2022"
            }
        }
    }
}