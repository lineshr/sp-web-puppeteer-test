node {

    def imageTag = "lineshr/sp-web-puppeteer-test:${env.BUILD_NUMBER}"
    def dockerHome = tool 'nyDocker'

    stage("Initializing") {
        //cleanWs();
        checkout scm;
        sh 'git reset --hard'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }

    stage("Building Images") {
        sh "docker build -t ${imageTag} -f docker/Dockerfile ."
    }

    stage("Running Tests CodeceptJS") {
        try {
            sh "run-final-tests.sh ${env.BUILD_NUMBER}"
        }
        finally {
         //   sh "ls report/"
            allure includeProperties: false, jdk: '', results: [[path: 'report']]
        }
    }


}
