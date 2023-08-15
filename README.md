Real time projpipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/your-username/your-repo.git']]])
            }
        }

        stage('Build') {
            steps {
                sh 'npm install' // Example: For a Node.js application
            }
        }

        stage('Test') {
            steps {
                sh 'npm test' // Example: Run tests using npm
            }
        }

        stage('Package') {
            steps {
                sh 'npm build' // Example: Create a build artifact
            }
        }

        stage('Deploy') {
            steps {
                sh 'npm deploy' // Example: Deploy to a testing environment
            }
        }

        stage('Deploy to Production') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('SUCCESS') }
            }
            steps {
                sh 'npm deploy production' // Example: Deploy to production
            }
        }
    }
}
ect
