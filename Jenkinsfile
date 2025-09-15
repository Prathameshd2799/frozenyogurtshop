pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Prathameshd2799/frozenyogurtshop.git'
        GIT_BRANCH = 'main'
        TOMCAT_APP_DIR = '/opt/tomcat/webapps/frozenyogurtshop'
        TOMCAT_SERVICE = 'tomcat'  // or tomcat9 depending on your system
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${env.GIT_BRANCH}",
                    url: "${env.GIT_REPO}"
            }
        }

        stage('Deploy Static Content') {
            steps {
                echo "Deploying content from ${env.GIT_REPO} (${env.GIT_BRANCH}) to ${env.TOMCAT_APP_DIR}"
                sh '''
                # Remove old files
                sudo rm -rf ${TOMCAT_APP_DIR}/*

                # Copy repo contents into Tomcat app directory
                sudo cp -r * ${TOMCAT_APP_DIR}/

                # Fix permissions
                sudo chown -R tomcat:tomcat ${TOMCAT_APP_DIR}
                sudo chmod -R 755 ${TOMCAT_APP_DIR}

                # Restart Tomcat
                sudo systemctl restart ${TOMCAT_SERVICE}
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful! Visit: http://<server-ip>:8080/frozenyogurtshop/'
        }
        failure {
            echo '❌ Deployment failed.'
        }
    }
}
