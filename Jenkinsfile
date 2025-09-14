pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/miairan/jenkins-demo.git'
            }
        }

        stage('Debug Environment') {
            steps {
                sh 'echo $PATH'
                sh 'which node || echo "node not found"'
                sh 'which npm || echo "npm not found"'
                sh 'node -v || echo "node not available"'
                sh 'npm -v || echo "npm not available"'
            }
        }
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
