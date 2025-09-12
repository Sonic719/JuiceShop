pipeline {
    agent none  // общий pipeline без дефолтного агента

    stages {
        stage('Checkout & Build') {
            agent { label 'master' }  // билд на мастере
            steps {
                git url: 'https://github.com/Sonic719/JuiceShop.git', branch: 'main'
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Send & Check on PT AI') {
            agent { label 'PT-AI-Agent' }  // агент Debian
            steps {
                // передать собранный билд на сервер PT AI
                sh 'scp -r /path/to/build jenkins@pt-ai-server:/check/path'
                // запустить проверку
                sh '/home/jenkins/pt-ai/run-check.sh /check/path'
            }
        }
    }

    post {
        success { echo '✅ Build & PT AI check done!' }
        failure { echo '❌ Something failed!' }
    }
}
