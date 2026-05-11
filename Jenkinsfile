pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/arn17-gamin/devops-158-DjondjueAurian-tp'
            }
        }

        stage('Install dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install flask
                '''
            }
        }

        stage('Restart Flask app') {
            steps {
                sh '''
                    pkill -f "python app.py" || true
                    . venv/bin/activate
                    nohup python app.py > flask.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            echo 'Déploiement automatique réussi ! BRAVO DAMN'
        }
        failure {
            echo 'Échec du pipeline. - AIE AIE AIE CA PUE'
        }
    }
}
