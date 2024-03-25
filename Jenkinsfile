node {
    def app
    
    stage('Clone repository') {
        when {
            branch 'dev' // Only trigger this stage for the 'dev' branch
        }
        steps {
            checkout scm
        }
    }
    
    stage('Build image') {
        when {
            branch 'dev' // Only trigger this stage for the 'dev' branch
        }
        steps {
            app = docker.build("paunovskidavid/kiii-lab4-new")
        }
    }
    
    stage('Push image') {
        when {
            branch 'dev' // Only trigger this stage for the 'dev' branch
        }
        steps {
            docker.withRegistry('https://registry.hub.docker.com', 'docker-creds') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                // signal the orchestrator that there is a new version
            }
        }
    }
}
