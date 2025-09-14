pipeline {
    agent any
    
    environment {
        // 确保每次执行都加载 nvm 目录（jenkins 用户下安装的）
        NVM_DIR = "${env.HOME}/.nvm"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/miairan/jenkins-demo.git'
            }
        }
        
        stage('Check nvm & Node.js') {
            steps {
                sh '''
                    # 加载 nvm
                    export NVM_DIR="$HOME/.nvm"
                    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"

                    echo "🔍 可用 Node.js 版本列表："
                    nvm ls

                    echo "⬇️  如果未安装则安装 Node.js 18.18.2..."
                    nvm install 18.18.2

                    echo "✅ 使用 Node.js 18.18.2"
                    nvm use 18.18.2

                    echo "🔎 当前 Node 版本："
                    node -v
                    echo "🔎 当前 npm 版本："
                    npm -v
                '''
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
