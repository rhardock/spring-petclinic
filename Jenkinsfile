pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')  // Trigger the pipeline every 10 minutes on Mondays
    }

    stages {
        stage('Build, Test & Generate Jacoco Report') {
            steps {
                script {
                    // Checkout the repository
                    checkout scm

                    // Run Maven build and generate Jacoco code coverage report
                    sh 'mvn clean install jacoco:report'
                }
            }
        }
    }

    post {
        always {
            // Archive the generated Jacoco report
            archiveArtifacts allowEmptyArchive: true, artifacts: 'target/site/jacoco/index.html', onlyIfSuccessful: true
            junit '**/target/test-classes/test-reports/*.xml'  // Archive test results
            echo 'Pipeline completed.'
        }
    }
}
