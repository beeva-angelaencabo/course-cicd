node('master') {
  stage('Checkout') {
    deleteDir()
    git credentialsId: '4401fb9e-6b42-4f87-a0de-092d7f5a35bf', url: 'git@github.com:beeva-angelaencabo/course-cicd.git'

  }
  stage('Test') {
    sh './simplehttpserver/tests/nittests.sh ./simplehttpserver/'
  }
}
