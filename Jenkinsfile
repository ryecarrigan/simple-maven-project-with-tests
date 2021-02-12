podTemplate(label: BUILD_TAG, containers: [containerTemplate(name: 'maven', image: 'maven', command: 'sleep', args: 'infinity')]) {
  node(BUILD_TAG) {
    checkout scm
    container('maven') {
      sh 'mvn -B -ntp -Dmaven.test.failure.ignore verify'
      sh 'mvn surefire-report:report'
    }
    junit '**/target/surefire-reports/TEST-*.xml'
    publishHTML reportDir: 'target/site', reportFiles: 'surefire-report.html', reportName: 'HTML Report'
  }
}
