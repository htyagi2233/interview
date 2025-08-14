pipeline {
    agent any

    environment {
        MAVEN_HOME = tool name: 'Maven-3.9', type: 'hudson.tasks.Maven$MavenInstallation'
        DEPLOY_SERVER = 'staging.example.com'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "📥 Checking out code from GitHub..."
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: 'main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/htyagi2233/interview.git',
                        credentialsId: 'github-pat' // ⬅️ GitHub credentials here
                    ]]
                ])
            }
        }

        stage('Build') {
            steps {
                echo "🏗️ Building project with Maven..."
                sh "${MAVEN_HOME}/bin/mvn clean package -DskipTests"
            }
        }

        stage('Test') {
            steps {
                echo "🧪 Running tests..."
                sh "${MAVEN_HOME}/bin/mvn test"
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            environment {
                DEPLOY_CRED = credentials('deploy-server-pass') // ⬅️ username + password
            }
            steps {
                echo "🚀 Deploying to ${DEPLOY_SERVER}..."
                sh """
                   sshpass -p '${DEPLOY_CRED_PSW}' \
                   ssh -o StrictHostKeyChecking=no ${DEPLOY_CRED_USR}@${DEPLOY_SERVER} 'mkdir -p /opt/app'
                   
                   scp -o StrictHostKeyChecking=no target/*.jar ${DEPLOY_CRED_USR}@${DEPLOY_SERVER}:/opt/app/
                """
            }
        }
    }

    post {
        success {
            mail to: 'htyagi1100@gmail.com',
                 subject: "✅ Build SUCCESS - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Good news! The build was successful.\nCheck it here: ${env.BUILD_URL}"
        }
        failure {
            mail to: 'htyagi1100@gmail.com',
                 subject: "❌ Build FAILED - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build failed. Please check console logs:\n${env.BUILD_URL}"
        }
    }

}