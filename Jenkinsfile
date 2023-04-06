pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "LocalMaven"
    }

    stages {
        stage('Build') {
            steps {
                script {
                    dir('my-app') {
                // To run Maven on a Windows agent, use
                 bat "mvn clean package"
                    }
                }
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'my-app/target/*.jar'
                }
            }
        }
    }
}
