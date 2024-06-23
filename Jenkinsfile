pipeline {
    agent { label 'jmeter_slave_node1'}
    tools {
        maven 'maven3.9.6' 
    }
    
    stages {
        stage('source') {
            steps {
                git url: 'https://github.com/shashikjenkis/Jmeter_maven_Automation.git',
                    branch: 'master'
            }
        }
        stage('verify') {
            steps {
                 sh "mvn verify"
            }
        }
    }

    post {
        always {
            script {
                def buildStatus = currentBuild.currentResult
                def consoleOutputUrl = "${env.BUILD_URL}console"
                emailext (
                    subject: "Build ${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                    body: """
                        <p>Build ${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'</p>
                        <p>Check console output at <a href="${consoleOutputUrl}">${consoleOutputUrl}</a></p>
                    """,
                    to: 'shashik064@gmail.com',
                    from: 'sender@example.com',
                    mimeType: 'text/html'
                )
            }
        }
    }
}
