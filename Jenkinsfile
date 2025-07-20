pipeline {
    agent any

    stages {
        stage('build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                dir('learn-jenkins-app') {
                    sh '''
                    ls -la
                    node -v
                    npm -v
                    npm ci
                    npm run build
                    '''
                }
            }
        }

        stage('test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                dir('learn-jenkins-app') {
                    sh '''
                    test -f build/index.html
                    npm test || true
                    '''
                }
            }
        }
    }
}
