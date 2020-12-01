pipeline {
  environment {
    DOCKER_REGISTRY = "repository-docker-push.braingroup.ch"
	DOCKER_REGISTRY_PULL = "repository-docker.braingroup.ch"
	CONTAINER_NAME = "cypressomnium-$BRANCH_NAME.toLowerCase()"
	DOCKER_CREDENTIAL = 'docker-nexus-registry'
  }
  stages {
    stage('Build Docker') {
      steps {
        script {
          docker.withRegistry( "https://" + DOCKER_REGISTRY_PULL, DOCKER_CREDENTIAL ) {
            dockerImage = docker.build( DOCKER_REGISTRY + "/" + CONTAINER_NAME, ".")
          }
        }
      }
    }
  }
}
