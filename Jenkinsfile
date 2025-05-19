pipeline {
    agent any

    tools {
        nodejs 'NodeJS_20' // Asegurate de tener configurado este nombre en "Global Tool Configuration"
    }

    environment {
        COLLECTION = 'collections/Restful_Booker_API.postman_collection.json'
        ENVIRONMENT = 'environments/Local_Dev.postman_environment.json'
        REPORT = 'reports/report.html'
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run API Tests') {
            steps {
                sh 'npx newman run $COLLECTION -e $ENVIRONMENT --reporters cli,html --reporter-html-export $REPORT'
            }
        }

        stage('Publish Report') {
            steps {
                publishHTML(target: [
                    reportName : 'Newman API Report',
                    reportDir  : 'reports',
                    reportFiles: 'report.html',
                    keepAll    : true,
                    alwaysLinkToLastBuild: true,
                    allowMissing: false
                ])
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'reports/*.html', fingerprint: true
        }
    }
}

