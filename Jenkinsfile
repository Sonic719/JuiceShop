pipeline {
    agent { label 'PT-AI-Agent' } // label твоего агента

    stages {
        stage('Checkout') {
            agent { label 'master' } // билд на мастере
            steps {
                git url: 'https://github.com/Sonic719/JuiceShop.git', branch: 'main'
            }
        }

        stage('Install & Build') {
            agent { label 'master' }
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Send to PT AI') {
            steps {
                // пример передачи на PT AI сервер
                sh 'scp -r build/* jenkins@pt-ai-server:/path/to/check/'
            }
        }

        stage('Run PT AI Check') {
            steps {
                // выполнить проверку на агенте
                sh '/home/jenkins/pt-ai/run-check.sh /path/to/check/'
            }
        }
    }

    post {
        success { echo '✅ Build & PT AI check completed!' }
        failure { echo '❌ Failed!' }
    }
}
