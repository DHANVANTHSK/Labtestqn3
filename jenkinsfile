pipeline {
    agent any

    environment {
        APP_NAME    = 'InventoryService'
        APP_VERSION = 'v2.4.0'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Fetching code from repository for ${env.APP_NAME}..."
                // This automatically clones the Git URL you provided in the Jenkins UI
                checkout scm 
            }
        }

        stage('Build') {
            steps {
                echo "Running a compilation check on app.py..."
                sh 'python3 -m py_compile app.py'
            }
        }

        stage('Deploy') {
            steps {
                input message: "Approve deployment of ${env.APP_NAME} version ${env.APP_VERSION}?", ok: 'Release'

                echo "Deployment approved! Executing application..."
                sh 'python3 app.py'
            }
        }
    }
}
