
pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Retrieving GrapeVista source code from GitHub...'
                checkout scm
                bat 'dir'
            }
        }

        stage('Build') {
            steps {
                echo 'Checking GrapeVista project files...'

                bat '''
                    if not exist index.html exit /b 1
                    if not exist app.py exit /b 1
                    if not exist README.md exit /b 1
                    echo All project files found.
                '''

                bat 'findstr /C:"GrapeVista" index.html'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing website content...'

                bat 'findstr /C:"Thompson Seedless" index.html'
                bat 'findstr /C:"Cabernet Sauvignon" index.html'

                echo 'Website content tests passed.'
            }
        }
    }

    post {
        success {
            echo 'GrapeVista Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check the Console Output.'
        }
    }
}
