pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven3.8"
    }

    stages {
        stage('Test') {
            input 'Do you want to proceed?'
        }
        
        stage ('pre-build') {
            parallel{
                stage ('unittest') {
                    echo 'I am in Unit Testing Phase'
                }
                stage ('integrationtest') {
                    echo 'I am in Integration Testing Phase'
                }
            }
        }
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/ResmiRamakrishnan780/BankAppRepo.git'

                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                 bat "mvn -f Day1-BankApp\\pom.xml -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'Day1-BankApp/target/*.jar'
                }
            }
        }
    }
}
