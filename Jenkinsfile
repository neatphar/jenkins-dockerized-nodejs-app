pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh """
                        docker build -t neatphar/nodejs-app .
                        docker login -u ${USERNAME} -p ${PASSWORD}
                        docker push neatphar/nodejs-app
                    """
                }
            }
        }
        stage('CD') {
            steps {
                sh """
                    docker rm --force NodeJsApp 2>> /dev/null 
                    docker run --name NodeJsApp -d -p 3000:3000 neatphar/nodejs-app
                """
            }
        }
    }
}
