pipeline {
    agent any
    stage('Debug Env') {
        steps {
            sh 'which node || echo node not found'
            sh 'which npm || echo npm not found'
        }
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
    }

    post {
        always {
            echo "构建完成"
        }
    }
}
