pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Берем код из репозитория
                git branch: 'main', url: 'https://github.com/Sonic719/JuiceShop.git'
            }
        }

        stage('Install dependencies') {
            steps {
                // Установка npm-зависимостей
                bat 'npm install'
            }
        }

        stage('Build') {
            steps {
                // Проверка сборки проекта
                bat 'npm run build'
            }
        }

        stage('Test') {
            steps {
                // Прогон тестов (если есть)
                bat 'npm test --passWithNoTests'
            }
        }
    }

    post {
        success {
            echo '✅ Build succeeded!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
