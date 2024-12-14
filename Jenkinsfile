pipeline{
    agent any

    stages{
        stage("Git stage"){
            step{
                git branch: 'main', credentialsId: 'docker-hub', url: 'https://github.com/22120330-22120341/ci-cd-project.git'
            }
        }
    }
}