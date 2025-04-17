pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clone Git repository
                checkout scm
            }
        }

        stage('Set Build Name') {
            steps {
                script {
                    // Lấy commit ID hiện tại (rút gọn 7 ký tự)
                    def commitId = sh(script: 'git rev-parse --short=7 HEAD', returnStdout: true).trim()

                    // Đặt lại tên build
                    currentBuild.displayName = "#${env.BUILD_NUMBER} - ${commitId}"
                }
            }
        }

        stage('Test') {
            steps {
                echo "Chạy unit test hoặc bất kỳ job test nào ở đây"
            }
        }
    }
}
