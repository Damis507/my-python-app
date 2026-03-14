Set-Content -Path C:\Users\jovan\my-python-app\Jenkinsfile -Encoding UTF8 -Value 'pipeline {
    agent any

    stages {
        stage("Clone") {
            steps {
                checkout scm
            }
        }
        stage("Tests") {
            steps {
                sh "pip3 install pytest --break-system-packages"
                sh "python3 -m pytest test_app.py -v"
            }
        }
    }

    post {
        success { echo "Pipeline termine avec succes !" }
        failure { echo "Pipeline en echec !" }
    }
}'