pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: '10', url: 'https://github.com/kuronek01/greetingapp.git'
            }
        }
        stage('Install Dependencies') {
    steps {
        sh '''
            python3 -m venv venv
            . venv/bin/activate
            pip install -r requirements.txt
        '''
    }
}

        stage('Run Tests') {
            steps {
                sh 'venv/bin/python -m pytest tests/'
            }
        }
        stage('Security Scan') {
            steps {
                sh 'venv/bin/bandit -r app/'
            }
        }
        stage('Code Analysis') {
  steps {
    withSonarQubeEnv('YourSonarServer') {
      sh 'venv/bin/sonar-scanner \
        -Dsonar.projectKey=greetingapp \
        -Dsonar.sources=app \
        -Dsonar.python.version=3.11'
    }
  }
}

    }
}
