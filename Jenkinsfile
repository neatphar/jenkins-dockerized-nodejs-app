node {
    stage('CI') {
        withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
            sh 'docker build -t neatphar/nodejs-app .'
            sh 'docker login -u ${USERNAME} -p ${PASSWORD}'
            sh 'docker push neatphar/nodejs-app'
        }
    }
    stage('CD') {
        sh 'docker rm --force NodeJsApp 2>> /dev/null'
        sh 'docker run --name NodeJsApp -d -p 3000:3000 neatphar/nodejs-app'
    }
}
