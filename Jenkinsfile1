pipeline {
    agent any   // कोई भी उपलब्ध Jenkins एजेंट पर रन होगा
    stages {
        stage('Build') {
            steps {
                echo 'प्रोजेक्ट का निर्माण हो रहा है...'  // हिंदी में संदेश
            }
        }
        stage('Test') {
            steps {
                echo 'टेस्ट चल रहे हैं...'  // हिंदी में संदेश
            }
        }
        stage('Deploy') {
            steps {
                echo 'एप्लिकेशन तैनात हो रही है...'  // हिंदी में संदेश
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

// pipeline {
//     agent any   // कोई भी available Jenkins agent पर run होगा
//     stages {
//         stage('Build') {
//             steps {
//                 echo 'Building the project...'
//             }
//         }
//         stage('Test') {
//             steps {
//                 echo 'Running tests...'
//             }
//         }
//         stage('Deploy') {
//             steps {
//                 echo 'Deploying application...'
//             }
//         }
//     }


// post {
//         success {
//             mail to: 'htyagi1100@gmail.com',
//                  subject: "✅ Build SUCCESS - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
//                  body: "Good news! The build was successful.\nCheck it here: ${env.BUILD_URL}"
//         }
//         failure {
//             mail to: 'htyagi1100@gmail.com',
//                  subject: "❌ Build FAILED - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
//                  body: "The build failed. Please check console logs:\n${env.BUILD_URL}"
//         }
//     }

// }
// // यह Jenkinsfile एक साधारण pipeline को परिभाषित करता है जिसमें तीन चरण हैं: Build, Test, और Deploy
// // प्रत्येक चरण में एक साधारण echo कमांड है जो उस चरण का विवरण देता है
// // आप इसे अपने प्रोजेक्ट के अनुसार अनुकूलित कर सकते हैं
// // यह Jenkinsfile आपके CI/CD प्रक्रिया को स्वचालित करने में मदद करेगा
// // आप इसे अपने प्रोजेक्ट के अनुसार अनुकूलित कर सकते हैं
// // यह Jenkinsfile आपके CI/CD प्रक्रिया को स्वचालित करने में मदद करेगा
// // आप इसे अपने प्रोजेक्ट के अनुसार अनुकूलित कर सकते हैं    