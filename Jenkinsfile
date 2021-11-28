pipeline {
  agent any
  stages {
    stage('Make') {
      steps {
        sh 'make'
      }
    }
    stage('Python tests') {
      steps {
        sh 'cd test && nosetests -v --with-xunit'
      }
    }
    stage('Generate doc') {
      steps {
        sh 'doxygen'
        sh 'tar -cf doc.tgz doc/'
      }
    }
  }
  post {
    always {
        archiveArtifacts artifacts: 'doc.tgz', fingerprint: false
        archiveArtifacts artifacts: 'test/nosetests.xml', fingerprint: true
        junit skipPublishingChecks: true, testResults: 'test/nosetests.xml'
    }
  }
}
