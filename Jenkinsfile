pipeline {
    agent any

    tools {
      nodejs 'nodejs-13.3.0'
    }

    environment {
      imageName = "localhost:5000/frontend"
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
        stage('Docker Build') {
            script {
                def newImages = docker.build imageName + ":$BUILD_NUMBER"
                newImages.push()
                newImages.push('latest')
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging....'
                sh 'npm run package'
                archiveArtifacts artifacts: '**/distribution/*.zip', fingerprint: true 
            }
        }
    }
}
