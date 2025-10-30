pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
               
                git branch: 'main', 
                    url: 'https://github.com/mohamed-zakaria-csed/jenkins-demo.git',
                    credentialsId: 'github-pat-for-jenkins'
            }
        }

        stage('Build') {
            steps {
                // إنشاء بيئة Python افتراضية
                bat 'python -m venv venv'
                // تثبيت التبعيات باستخدام pip
                bat '.\\venv\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Run App') {
            steps {
                // تشغيل التطبيق داخل البيئة الافتراضية
                bat '.\\venv\\Scripts\\python app.py'
            }
        }

        stage('Deploy (Optional)') {
            when {
                expression { return false }  // نفعّلها لاحقاً عند الحاجة للنشر الفعلي
            }
            steps {
                echo 'Deploying...'
            }
        }
    }

    post {
        always {
            // تنظيف مساحة العمل بعد كل عملية بناء
            cleanWs()
        }
    }
}
