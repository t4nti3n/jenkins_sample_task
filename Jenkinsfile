pipeline {
    agent { label 'linux' }
    stages {
        stage('Set Custom Build Name') {
            steps {
                script {
                    // Lấy PR number, nếu không có thì mặc định là "noPR"
                    def prNum = env.CHANGE_ID ?: "noPR"
                    
                    // Lấy tên nhánh đích của PR (ví dụ: main, master)
                    def targetBranch = env.CHANGE_TARGET ?: "main" // Fallback là "main" nếu không có CHANGE_TARGET
                    
                    // Lấy Commit ID của nhánh đích
                    def commitID = sh(script: "git rev-parse origin/${targetBranch}", returnStdout: true).trim()?.take(7) ?: "noCommit"
                    
                    // Đặt tên build
                    currentBuild.displayName = "${env.BUILD_NUMBER}-PR-${prNum}-${commitID}"
                    
                    // In thông tin để debug
                    echo "PR Number: ${prNum}, Target Branch: ${targetBranch}, Commit: ${commitID}"
                    echo "Build Display Name: ${currentBuild.displayName}"
                }
            }
        }
    }
}