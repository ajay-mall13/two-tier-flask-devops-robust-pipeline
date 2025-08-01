pipeline {
    agent any


    stages {
        stage('Code Clone') {
            steps {
                git url: 'https://github.com/ajay-mall13/two-tier-flask-devops-robust-pipeline.git', branch: 'master'
            }
        }

        stage('Code Build') {
            steps {
                sh 'docker build -t my-app .'
            }
        }

        stage('test') {
            steps {
   		echo "devloper test dega"
            }
        }


    stage('Docker Build and Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerHubCreds',
                    usernameVariable: 'dockerHubUser',
                    passwordVariable: 'dockerHubPass'
                )]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker image tag my-app ${env.dockerHubUser}/two-tier-flask-app:latest"
                    sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                }
            }
        }


        stage('Code Deploy') {
            steps {
                sh 'docker compose up -d --build flask-app'
            }
        }
    }
}
                                                                                                                                                                                           
