pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/robertoit42/spanish-word-flip-flash.git'
            }
        }

        stage('build') {
            agent {
                docker {
                    image 'node:22-alpine'
                }
            }
            steps {
                ansiColor('xterm') {
                    sh 'npm ci'
                    sh 'npm run build'
                }
            }
        }

        stage('test') {
            parallel {
                stage('unit tests') {
                    agent {
                        docker {
                            image 'node:22-alpine'
                            reuseNode true
                        }
                    }
                    steps {
                        ansiColor('xterm') {
                            sh 'npx vitest run --reporter=verbose'
                        }
                    }
                }
            }
        }

        stage('deploy') {
            agent {
                docker {
                    image 'alpine'
                }
            }
            steps {
                ansiColor('xterm') {
                    echo 'Mock deployment was successful!'
                }
            }
        }
    }
}
