pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh """
                        docker build -t neatphar/nodejs-app .
                        docker login -u ${USERNAME} -p ${PASSWORD}
                        docker push
                    """
                }
            }
        }
        stage('CD') {
            steps {
                sh """
                    docker rm --force NodeJsApp 2>> /dev/null
                    docker run --name NodeJsApp -d -p 3030:3030 neatphar/nodejs-app
                """
            }
        }
    }
}
