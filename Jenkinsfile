pipeline {
    agent any

    tools {
        nodejs 'NodeJS 18' // Make sure this tool is configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vikashkr1101/myrepo.git', credentialsId: 'my-gitaccount-crendentials'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install' // Or 'yarn install' if you use Yarn
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build' // Or 'yarn build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm run test:unit' // Or 'yarn test:unit' or other test command
            }
        }

        stage('SonarQube Analysis') {
            steps {
               withSonarQubeEnv(credentialsId: 'sonarqube-token', installationName: 'MySonarQubeServer') {
                    sh '''
                        sonar-scanner \
                            -Dsonar.projectKey=mytodoapp \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.login=sqp_bc7057391a211e76cde5b9cede30b35a732d76a8
                    '''
                }
            }
        }
    }
}
