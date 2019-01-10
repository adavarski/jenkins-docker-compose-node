node {
   try {
     stage('Clone') {
       stage 'Checkout'
        checkout scm
     }
     stage('Integration Test') {
       sh "docker-compose -f docker-compose-ci-test.yaml up -d"
       sh "docker wait jenkins-docker-compose-node_integration_test_1"
     }
     stage('Deploy') {
       sh "docker build ."
     }
   } catch (e) {
     currentBuild.result = 'FAILURE'
     throw e
   } finally {
       sh "docker-compose -f docker-compose-ci-test.yaml down"
   }
}
