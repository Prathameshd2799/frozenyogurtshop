pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Prathameshd2799/frozenyogurtshop.git'
        TOMCAT_APP_DIR = '/opt/tomcat/webapps/frozenyogurtshop'
        TOMCAT_SERVICE = 'tomcat'  
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: env.GIT_REPO
            }
        }

        stage('Deploy Static Content') {
            steps {
                echo "Deploying content from ${env.GIT_REPO} to ${env.TOMCAT_APP_DIR}"
                sh '''
                # Remove the old content
                sudo rm -rf ${TOMCAT_APP_DIR}/*

                # Copy everything from the workspace to the Tomcat app directory
                sudo cp -r * ${TOMCAT_APP_DIR}/

               }
        }
    }

    post {
        success {
            echo '✅ Deployment successful! Visit http://34.227.75.252:8081/frozenyogurtshop/'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
