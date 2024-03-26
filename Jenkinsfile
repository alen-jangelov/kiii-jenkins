node {
    def app
    stage('Cloning our Git') { 
        steps { 
            git 'https://github.com/alen-jangelov/kiii-jenkins.git' 
        }
    } 
    stage('Build image') {
       app = docker.build("alenjangelov9720/kiii-jenkins")
    }
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}
