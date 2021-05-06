pipeline {
    environment {
        //This variable need be tested as string
        varError = '0'
    }

    agent any

    stages {
        stage('Error') {
            when {
                expression { varError == '1' }
            }
            steps {
                echo "Failure"
                error "failure test. It's work"
            }
        }

        stage('Success') {
            when {
                expression { varError == '0' }
            }
            steps {
                echo "ok"
            }
        }
    }
        post {
        always {
            echo 'Hello again! I  am here just to check if you get an email... disregard any contents'

            emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}",
                to: 'rajpalmanish@gmail.com, jayashree.bondre@iths.se, shubhangi.patil@iths.se, feng.zhu@iths.se, victor.hedstrom@iths.se, maria.shishkina@iths.se, elias.arezomande@iths.se'

        }
    }
}