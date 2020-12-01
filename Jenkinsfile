pipeline {
  environment {
    DOCKER_REGISTRY = "repository-docker-push.braingroup.ch"
	DOCKER_REGISTRY_PULL = "repository-docker.braingroup.ch"
	CONTAINER_NAME = "cypressomnium-$BRANCH_NAME".toLowerCase()
	DOCKER_CREDENTIAL = 'docker-nexus-registry'
  }
  agent { label 'master'}

  parameters {
    choice(name: 'numContainers', choices: ['1', '2', '3', '4', '5'], description: 'Enter number of containers needed')
    choice(name: 'reportState', choices: ['new', 'update'], description: 'Enter whether new or update report')
  }

  stages {
    stage ('Initialize') {
      steps {
        sh '''
            echo "PATH = ${PATH}"
          '''
      }
    }
    stage('Build Docker') {
      steps {
        script {
          docker.withRegistry( "https://" + DOCKER_REGISTRY_PULL, DOCKER_CREDENTIAL ) {
            dockerImage = docker.build( DOCKER_REGISTRY + "/" + CONTAINER_NAME, ".")
          }
        }
      }
    }
  stage('Push Docker') {
    steps {
      script {
        docker.withRegistry( "https://" + DOCKER_REGISTRY, DOCKER_CREDENTIAL ) {
          dockerImage.push()
        }
      }
    }
  }
    stage('Remove Unused docker image') {
      steps {
        sh "docker rmi $DOCKER_REGISTRY/$CONTAINER_NAME"
      }
    }

//    stage('Run cypress containers on Dione') {
//      steps {
//        script {
//          // Get user input on how many containers need to run
//          def numContainers = input(id: 'userInput', message: 'Enter number of containers needed',
//            parameters: [choice(choices: ['1', '2', '3', '4', '5'].join('\n'), description: '', name: 'numContainers')])
//          echo "Selected number of containers: ${numContainers}"
//
//          // Get user input on the status of build type
//          def reportState = input(id: 'userInput', message: 'Enter whether new or update report',
//            parameters: [choice(choices: ['new', 'update'].join('\n'), description: '', name: 'reportState')])
//          echo "Report selected: ${reportState}"
//
//          sh "cd /opt/docker-scripts/ansible/cypress/ && ansible-playbook -i hosts.conf run_cypress.yml --extra-vars 'count=${numContainers} build=$BUILD_NUMBER state=${reportState}'"
//        }
//      }
//    }
    stage('Run cypress containers on Dione') {
      steps {
        script {
          echo "Selected number of containers: ${numContainers}"
          echo "Report selected: ${reportState}"

          sh "cd /opt/docker-scripts/ansible/cypress/ && ansible-playbook -i hosts.conf run_cypress.yml --extra-vars 'count=${numContainers} build=$BUILD_NUMBER state=${reportState} branch_orig=$BRANCH_NAME'"
        }
      }
    }


  }
}
