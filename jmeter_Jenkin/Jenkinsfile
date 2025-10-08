pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Check out the code from your Git repository
                git url: 'https://github.com/YethiPT-Team/Test_Jmx_repo/tree/main/jmeter_Jenkin.git',
                    branch: 'main'
            }
        }

        stage('Run JMeter Test') {
            steps {
                script {
                    def jmeterHome = tool 'jmeter' // Specify the name of your JMeter tool configuration in Jenkins
                    sh "${jmeterHome}/bin/jmeter.sh -n -t C:/PT/Grafana_JMeter.jmx -l C:/PT/Jenkins/results.jtl -e -o C:/PT/Jenkins/reports"
                }
            }
        }

        stage('Publish Performance Report') {
            steps {
                // The performance plugin will read the results.jtl and display a report
                publishPerformanceReport(
                    reportFile: 'results.jtl'
                )
                // Archive the generated HTML report for later viewing
                archiveArtifacts(
                    artifacts: 'reports/**/*',
                    fingerprint: true
                )
            }
        }
    }
}
