pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "LocalMaven"
    }

    stages {      
              stage("Maven Build") {
            steps {
                script {
                dir('my-app') {
                    bat "mvn -Dmaven.test.failure.ignore=true clean package"
                }
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
