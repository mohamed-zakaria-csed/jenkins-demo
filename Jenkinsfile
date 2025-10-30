pipeline {
    agent any
    
    // تعريف متغير بيئة PYTHON_HOME بمسار Python المحدد
    environment {
        // المسار الصحيح لملف python.exe على نظام التشغيل Windows
        PYTHON_HOME = 'C:\\Users\\MicroTech\\AppData\\Local\\Programs\\Python\\Python313\\python.exe' 
    }

    stages {
        stage('Clone Repository') {
            steps {
                // سحب الكود من GitHub باستخدام بيانات الاعتماد (PAT)
                git branch: 'main', 
                    url: 'https://github.com/mohamed-zakaria-csed/jenkins-demo.git',
                    credentialsId: 'github-pat-for-jenkins'
            }
        }

        stage('Build') {
            steps {
                // إنشاء بيئة Python افتراضية باستخدام المسار الكامل لـ PYTHON_HOME
                bat "${env.PYTHON_HOME} -m venv venv"
                
                // تثبيت التبعيات (pip في البيئة الافتراضية)
                bat '.\\venv\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Run App') {
            steps {
                // تشغيل التطبيق داخل البيئة الافتراضية
                // نستخدم مسار python داخل venv بعد أن تم إنشاؤه بنجاح
                bat '.\\venv\\Scripts\\python app.py'
            }
        }

        stage('Deploy (Optional)') {
            when {
                expression { return false }  // معطلة حالياً
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
