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

// NOUVEAU STAGE : Tests unitaires
stage('Run unit tests') {
    steps {
        sh '''
            source venv/bin/activate
            python -m pytest test_app.py -v --tb=short
        '''
    }
    post {
        success {
            echo 'Tous les tests unitaires sont passés avec succès !'
        }
        failure {
            echo 'Échec des tests unitaires. Le déploiement est annulé.'
        }
    }
}
