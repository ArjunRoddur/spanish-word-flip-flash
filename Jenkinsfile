pipeline {
    agent any
    
    options {
        ansiColor('xterm')
    }

    stages {
        stage('build and test') {
            agent {
                docker {
                    image 'node:22-alpine'
                }
            }
            steps {
                sh 'npm ci --include=dev'
                sh 'npm run build'
                sh 'npm run test:unit -- --reporter=verbose'
            }
        }
        stage('integration test'){
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.54.2-jammy'
                    resuseNode true

                }
            }
            steps {
                sh 'npx playwright test'
                }
        }

        stage('deploy') {
            agent {
                docker {
                    image 'alpine'
                }
            }
            steps {
                // Mock deployment which does nothing
                echo 'Mock deployment was successful!'
            }
        }
    }
}