pipeline {
    agent any
    
    environment {
        // Static environment variables
        MAVEN_HOME = tool name: 'Maven-3.9', type: 'hudson.tasks.Maven$MavenInstallation'
        DEPLOY_SERVER = 'staging.example.com'
        
        // Secure credentials
        GITHUB_TOKEN = credentials('github-token')
        DEPLOY_CRED = credentials('deploy-server-pass')
    }
    
    stages {
        
        stage('Checkout') {
            steps {
                echo "📥 Checking out code from GitHub..."
                git branch: 'main',
                    url: "https://username:${GITHUB_TOKEN}@github.com/your-username/your-repo.git"
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
            steps {
                echo "🚀 Deploying to ${DEPLOY_SERVER}..."
                sh """
                   sshpass -p '${DEPLOY_CRED_PSW}' \
                   ssh ${DEPLOY_CRED_USR}@${DEPLOY_SERVER} 'mkdir -p /opt/app && exit'
                   scp target/*.jar ${DEPLOY_CRED_USR}@${DEPLOY_SERVER}:/opt/app/
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