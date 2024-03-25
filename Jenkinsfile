node {
    def app
    
    stage('Clone repository') {
        if (env.BRANCH_NAME == 'dev') {
            // Your clone repository steps here
            checkout scm
        }
    }
    
    stage('Build image') {
        if (env.BRANCH_NAME == 'dev') {
            // Your build image steps here
            app = docker.build("paunovskidavid/kiii-lab4-new")
        }
    }
    
    stage('Push image') {
        if (env.BRANCH_NAME == 'dev') {
            // Your push image steps here
            docker.withRegistry('https://registry.hub.docker.com', 'docker-creds') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                // signal the orchestrator that there is a new version
            }
        }
    }
}
