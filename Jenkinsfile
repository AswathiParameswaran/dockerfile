pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker-compose build
            }
        }

        stage('Run') {
            steps {
                sh 'docker-compose up -d'
            }
        }

        stage('Test') {
            steps {
                script {
                    def status = sh(script: 'curl -s -o /dev/null -w "%{http_code}" http://localhost:8000', returnStatus: true)
                    if (status != 200) {
                        error "WordPress app not running, returned HTTP status code ${status}"
                    }
                }
            }
        }
    }

    post {
        always {
            sh 'docker-compose down'
        }
    }
}
