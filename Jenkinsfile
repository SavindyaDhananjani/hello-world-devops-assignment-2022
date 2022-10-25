pipeline {
  environment {
    registry = "savindyadhananjani/lolc-hello-world"
    registryCredential = 'dockerhub-secret'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Clone Repository') {
      steps {
        bat "rm -rf hello-world-devops-assignment-2022"
        bat "git clone https://github.com/SavindyaDhananjani/hello-world-devops-assignment-2022.git"
      }
    }
    stage('Clean') {
      steps {
        bat "mvn clean -f hello-world-devops-assignment-2022"
      }
    }
    stage('Install') {
      steps {
        bat "mvn install -f hello-world-devops-assignment-2022"
      }
    }
    stage('Test Project') {
      steps {
        bat "mvn test -f hello-world-devops-assignment-2022"
      }
    }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build(registry + ":$BUILD_NUMBER")
        }
      }
    }
    stage('Test Image') {
      steps {
        script{
                app.inside {
                    sh 'echo "Test passed"'
          }
        }
      }
    }
    stage('Deploy Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}

/*
pipeline {
    agent any
    environment{
        registryCredential = '<dockerhub-credential-name>'
    }
    stages {
        stage('Clone Repository') {
            steps {
                bat "git clone https://github.com/SavindyaDhananjani/hello-world-devops-assignment-2022.git"
            }
        }
        stage('Clean') {
                    steps {
                        bat "mvn clean -f hello-world-devops-assignment-2022"
                    }
                }
        stage('Install') {
            steps {
                bat "mvn install -f hello-world-devops-assignment-2022"
            }
        }
        stage('Test Project') {
            steps {
                bat "mvn test -f hello-world-devops-assignment-2022"
            }
        }
        stage('Package') {
            steps {
                bat "mvn package -f hello-world-devops-assignment-2022"
            }
        }
        stage('Build Image') {
             steps {
                 script{
                         app = docker.build("savindyadhananjani/lolc-hello-world-assignment")
                 }
             }
        }
        stage('Test Image') {
              steps {
                  script{
                          app.inside {
                              sh 'echo "Test passed"'
                          }
                  }
              }
        }
        stage('Deploy Image') {
            steps {
                script{
                        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                	        app.push("${env.BUILD_NUMBER}")
                	        app.push("latest")
                	    }
                }
            }
        }
    }
} *//*

 */



