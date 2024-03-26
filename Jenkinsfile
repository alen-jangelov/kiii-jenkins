node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("alenjangelov9720/kiii-jenkins")
    }
    stage('Push image') {   

        when{expression {env.BRANCH_NAME == 'dev'}}       
              steps('Execute'){
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                    app.push("${env.BRANCH_NAME}-latest")
                    // signal the orchestrator that there is a new version
                } 
        }
    }
}
