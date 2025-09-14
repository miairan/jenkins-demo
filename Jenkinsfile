pipeline {
    agent any
    
    environment {
        // 确保每次执行都加载 nvm 目录（jenkins 用户下安装的）
        NVM_DIR = "${env.HOME}/.nvm"
    }

    options {
        shell '/bin/bash' // 一定要加这行
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
                    echo "👉 当前用户是：$(whoami)"
                    echo "👉 NVM_DIR=$NVM_DIR"
                    ls -la $NVM_DIR

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

        stage('Install Dependencies') {
            steps {
                sh '''
                    export NVM_DIR="$HOME/.nvm"
                    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
                    nvm use 18.18.2

                    npm install
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    export NVM_DIR="$HOME/.nvm"
                    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
                    nvm use 18.18.2

                    npm test
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                    export NVM_DIR="$HOME/.nvm"
                    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
                    nvm use 18.18.2

                    npm run build
                '''
            }
        }
    }

    post {
        always {
            echo "构建完成"
        }
    }
}
