node {
    def app
    
    stage('Clone repository') {
        when {
            expression {
                env.BRANCH_NAME == 'dev'
            }
        }

        steps {
            checkout scm
        }
    }
    
    stage('Build image') {
        when {
            expression {
                env.BRANCH_NAME == 'dev'
            }
        }

        steps {
            app = docker.build("paunovskidavid/kiii-lab4-new")
        }
    }
    
    stage('Push image') {
        when {
            expression {
                env.BRANCH_NAME == 'dev'
            }
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
