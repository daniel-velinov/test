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
  agent any
  parameters {
    choice(name: 'numContainers', choices: ['1', '2', '3', '4', '5'], description: 'Enter number of containers needed')
    choice(name: 'reportState', choices: ['new', 'update'], description: 'Enter whether new or update report')
	text(name: 'propertyFile', defaultValue: '', description: 'Enter Propertyfiles as raw text')
  }

  stage('Run cypress containers on Dione') {
    steps {
      script {
          echo "Selected number of containers: ${numContainers}"
          echo "Report selected: ${reportState}"
          echo "Propertyfiles entered: ${propertyFile}"
		  sh "echo ${propertyFile} > /tmp/propertyFile.js"
		//  sh "echo '${propertyFile}' > propertyFile-$BUILD_NUMBER.js"
		 // sh "echo '${propertyFile}' > propertyFile-$BUILD_NUMBER.js"
		  // sh "cd /tmp && ansible-playbook -i hosts.ini test.yml --extra-vars 'count=${numContainers} build=$BUILD_NUMBER state=${reportState}'"
        }
      }
    }
  }
}
