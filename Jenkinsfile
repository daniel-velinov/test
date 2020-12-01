pipeline {
  environment {
    BRANCH_VALID = "$BRANCH_NAME".replaceAll('/','-').toLowerCase()
    DOCKER_REGISTRY = "repository-docker-push.braingroup.ch"
    DOCKER_REGISTRY_PULL = "repository-docker.braingroup.ch"
    CONTAINER_NAME = "cypressomnium-$BRANCH_VALID"
    DOCKER_CREDENTIAL = 'docker-nexus-registry'
  }
	
  agent any
  parameters {
    choice(name: 'numContainers', choices: ['1', '2', '3', '4', '5'], description: 'Enter number of containers needed')
    choice(name: 'reportState', choices: ['new', 'update'], description: 'Enter whether new or update report')
    text(name: 'propertyFile', defaultValue: '', description: 'Enter Propertyfiles as raw text')
  }
 stages {
  stage('Run cypress containers on Dione') {
    steps {
      script {
          echo "Selected number of containers: ${numContainers}"
          echo "Report selected: ${reportState}"
	  echo "Propertyfile data: ${propertyFile}"
	      echo "$BRANCH_VALID"
	      echo "$CONTAINER_NAME"
	      
          sh '''cat <<EOF > /tmp/propertyFile-$BRANCH_VALID.js 
${propertyFile}
	      '''	      
	      		  // sh "cd /tmp && ansible-playbook -i hosts.ini test.yml --extra-vars 'count=${numContainers} build=$BUILD_NUMBER state=${reportState}'"
        }
      }
    }
  }
}
