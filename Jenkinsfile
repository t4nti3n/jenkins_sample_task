pipeline {
    agent any

    stages {
        stage('Checkout Repo') {
            steps {
                checkout scm
            }
        }
        stage('Run Script 1') {
            steps {
                script {
                    catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                        sh 'echo Running Script 1 > script1.log'
                    }
                }
            }
        }
        stage('Run Script 2') {
            when {
                expression { currentBuild.result == 'FAILURE' }
            }
            steps {
                sh 'echo Running Script 2 > script2.log'
            }
        }
        stage('Run Script 3') {
            steps {
                sh 'echo Running Script 3 > script3.log'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'script3.log', allowEmptyArchive: true
        }
    }
}
