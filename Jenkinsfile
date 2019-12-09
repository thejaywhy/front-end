pipeline {
    agent any

    tools {
      nodejs 'nodejs-13.3.0'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'npm install' 
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'npm run test'
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging....'
                sh 'npm run package'
                archiveArtifacts artifacts: '**/distribution/*.zip', fingerprint: true 
            }
        }
        stage('Docker Build') {
            steps {
                def newImages = docker.build("localhost:5000/frontend:${env.BUILD_ID}")
                newImages.push()
                newImages.push('latest')
            }
        }
    }
}
