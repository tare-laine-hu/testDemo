pipeline {
    agent any
    stages {
        stage('Deploying') {
            steps {
                echo 'Buiding the application'
            }
        }
        stage('Testing') {
            steps {
                bat 'npm i'
                bat 'npx cypress run --reporter junit --reporter-options "mochaFile=reports/junit-[hash].xml"'
            }
        }
        stage('Uploading into TestRail') {
                steps {
                echo 'Uploading into TestRail'
                bat trcli -y -c "trcli-config.yml" parse_junit -f "reports/junit*.xml"
                }
        }
    }
    post {
        always {
            /* groovylint-disable-next-line LineLength */
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'cypress/report', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
        }
    }
}
