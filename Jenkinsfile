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
        stage('runPerformanceTests') {
            steps {
                // Run JMeter tests and save the results to a specific file
                sh "mvn jmeter:jmeter -Dlog_file=results.jtl"
            }
        }
        stage('publishPerformanceReport') {
            steps {
                script {
                    // Use the performance plugin to publish test results
                    perfReport errorFailedThreshold: 0, 
                               errorUnstableThreshold: 0, 
                               relativeFailedThresholdPositive: 1.0, 
                               relativeUnstableThresholdPositive: 0.2, 
                               sourceDataFiles: 'results.jtl'
                }
            }
        }
         stage('archiveArtifacts') {
            steps {
                 archiveArtifacts artifacts: 'target'
            }
        }
    }
    
    }

