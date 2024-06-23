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
         stage('archiveArtifacts') {
            steps {
                 archiveArtifacts artifacts: 'target/*.jar'
            }
        }
    }
    
    }

