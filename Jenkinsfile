pipeline {
    agent any // Use any available agent

    stages {
        stage('Checkout') {
            steps {
                // Checkout from Git (replace with your repository details)
                git branch: 'main', url: 'https://github.com/vikashkr1101/myrepo.git', credentialsId: 'my-gitaccount-crendentials'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the project...'

                // Example build steps (adapt to your project):
                // For a .NET project:
                // bat 'dotnet build MySolution.sln' 

                // For a Node.js/Vue.js project:
                sh 'npm install' // or yarn install
                sh 'npm run build' // or yarn build

            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'

                // Example test steps (adapt to your project):
                // For a .NET project:
                // bat 'dotnet test MySolution.sln'

                // For a Node.js/Vue.js project:
                sh 'npm test' // or yarn test
            }
        }
        stage('SonarQube Analysis') {
            steps {
               withSonarQubeEnv('My SonarQube Server') { // Name from step 2
                        bat '''
                        "C:\\path\\to\\sonar-scanner-msbuild\\SonarScanner.MSBuild.exe" begin /k:"YOUR_PROJECT_KEY_C#" /d:sonar.host.url="http://localhost:9000" /d:sonar.login="YOUR_SONAR_TOKEN"
                        "C:\\path\\to\\dotnet\\dotnet.exe" build MySolution.sln
                         "C:\\path\\to\\sonar-scanner-msbuild\\SonarScanner.MSBuild.exe" end
                        '''
                    }
                }
            }
    }
}
