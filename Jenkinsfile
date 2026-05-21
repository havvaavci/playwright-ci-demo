pipeline {
    agent any

    options {
        timestamps()
        ansiColor('xterm')
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Kodlar çekiliyor...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Node modülleri yükleniyor...'
                bat 'npm ci'
            }
        }

        stage('Install Playwright Browsers') {
            steps {
                echo 'Playwright browserları yükleniyor...'
                bat 'npx playwright install --with-deps'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Testler çalıştırılıyor...'
                bat 'npx playwright test --reporter=line'
            }
            post {
                always {
                    echo 'Test sonuçları arşivleniyor...'
                    archiveArtifacts artifacts: 'playwright-report/**', allowEmptyArchive: true
                    junit 'test-results/**/*.xml'
                }
            }
        }
    }
}
