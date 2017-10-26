node {
  stage('clear work space') {
    cleanWs()
  }
  stage('test') {
    sh 'echo "test"'
  }
  stage('pull artifact') {
    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'nexus',
                  usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']])
  }
        //sh 'curl -GET -u  ${USERNAME}:${PASSWORD} "http://nexus-2040588938.ca-central-1.elb.amazonaws.com/repository/hgallotest/nexus/PR-2/${env.REVISION}/${env.ARTIFACT}-${env.REVISION}.jar" -O'
  sh 'curl -GET -u  ${USERNAME}:${PASSWORD} "http://nexus-2040588938.ca-central-1.elb.amazonaws.com/repository/hgallotest/nexus/spring-boot-rest-example/master-build-6/spring-boot-rest-example-master-build-6.jar" -O'

  stage("deploy") {
    pushToCloudFoundry cloudSpace: 'stage',
                       credentialsId: 'pws',
                       organization: 'Spinnaker_POC',
                       selfSigned: true,
                       target: 'https://api.run.pivotal.io'
  }
}
