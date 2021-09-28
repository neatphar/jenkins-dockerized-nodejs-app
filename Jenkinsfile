node {
    stage('CI') {
        sh "git init"
        sh "git remote add origin https://github.com/neatphar/jenkins-dockerized-nodejs-app.git 2>> /dev/null"
        sh "git fetch"
        sh "git checkout origin/scripted -ft"
        withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
            sh 'docker build -t neatphar/nodejs-app .'
            sh 'docker login -u ${USERNAME} -p ${PASSWORD}'
            sh 'docker push neatphar/nodejs-app'
        }
    }
    stage('CD') {
        sh 'docker rm --force NodeJsApp 2>> /dev/null'
        sh 'docker run --name NodeJsApp -d -p 4000:4000 neatphar/nodejs-app'
    }
}
