pipeline {
    agent any

    tools {
        nodejs "NodeJS 20" // asegúrate que este nombre coincida con la instalación configurada en Jenkins
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run API Tests') {
            steps {
                sh 'mkdir -p reports' // crea carpeta si no existe
                sh 'npm run api-test'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'reports/*.html', fingerprint: true
            publishHTML([
                reportDir: 'reports',
                reportFiles: 'report.html',
                reportName: 'Newman API Report'
            ])
        }
    }
}

