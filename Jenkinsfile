pipeline{
    agent any
    environment{
        USERNAME = '22120330'
        PASSWORD = 'Thai668084'
    }
    stages{
        stage("Git stage"){
            steps{
                git branch: 'main', credentialsId: 'docker-hub', url: 'https://github.com/22120330-22120341/ci-cd-project.git'
            }
        }
        stage("Image build"){
            steps{
                sh 'docker image build -t 22120330/ci-cd-project:v$BUILD_ID .'
                sh 'docker image tag 22120330/ci-cd-project:v$BUILD_ID 22120330/ci-cd-project:latest'
            }
        }
        stage("Image push"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'Thai668084', usernameVariable: '22120330')]) {
                    sh """
                echo $PASSWORD | docker login -u $USERNAME --password-stdin
                """
                    sh 'docker image push 22120330/ci-cd-project:v$BUILD_ID'
                    sh 'docker image push 22120330/ci-cd-project:latest'

                }
            }
        }
        stage("Container creating") {
            steps {
                script {
                    def containerExists = sh(
                        script: "docker ps -q -a --filter 'name=ci-cd-project'",
                        returnStdout: true
                    ).trim()

                    if (containerExists) {
                        echo "Stopping and removing existing container"
                        sh 'docker stop ci-cd-project || true'
                        sh 'docker rm ci-cd-project || true'
                    } else {
                        echo "No existing container found"
                    }
                }
                sh 'docker run -itd --name ci-cd-project -p 8600:3000 22120330/ci-cd-project:latest'
            }
        }
    }
}