pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/mohamed-zakaria-csed/jenkins-demo.git'
		credentialsId: 'github-pat-for-jenkins'
            }
        }

        stage('Build') {
            steps {
                bat 'python -m venv venv'
                bat '.\\venv\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Run App') {
            steps {
                bat '.\\venv\\Scripts\\python app.py'
            }
        }

        stage('Deploy (Optional)') {
            when {
                expression { return false }  // نفعّلها بعدين
            }
            steps {
                echo 'Deploying...'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
