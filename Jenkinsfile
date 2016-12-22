node('master') {
  stage('Checkout') {
    deleteDir()
    git credentialsId: '4401fb9e-6b42-4f87-a0de-092d7f5a35bf', url: 'git@github.com:beeva-angelaencabo/course-cicd.git'

  }
  stage('Test') {
    sh './simplehttpserver/tests/unittests.sh ./simplehttpserver/'
  }
  stage('Package and publish') {
    sh "tar -zcvf simplehttpserver-${env.JOB_NAME}-${env.BUILD_ID}.tar.gz ./simplehttpserver"
    sh "aws s3 cp simplehttpserver-${env.JOB_NAME}-${env.BUILD_ID}.tar.gz s3://clase-gendevops2-cicd-ci/"
  }
  stage('Deploy') {
    sh "aws s3 cp s3://clase-gendevops2-cicd-ci/simplehttpserver-${env.JOB_NAME}-${env.BUILD_ID}.tar.gz /tmp/"
    sh "mkdir /opt/${env.JOB_NAME}-${env.BUILD_ID}"
    sh "mkdir -p /tmp/simplehttpserver/${env.JOB_NAME}-${env.BUILD_ID}"
    sh "tar -zxvf /tmp/simplehttpserver-${env.JOB_NAME}-${env.BUILD_ID}.tar.gz -C /tmp/simplehttpserver/${env.JOB_NAME}-${env.BUILD_ID}/"

    sh "mv /tmp/simplehttpserver/${env.JOB_NAME}-${env.BUILD_ID}/simplehttpserver/* /opt/${env.JOB_NAME}-${env.BUILD_ID}/"
    sh "rm -rf /opt/${env.JOB_NAME}-${env.BUILD_ID}/tests"

    sh "mv /opt/${env.JOB_NAME}-${env.BUILD_ID}/httpserver.py /opt/${env.JOB_NAME}-${env.BUILD_ID}/httpserver-${env.JOB_NAME}.py"
  }
}
