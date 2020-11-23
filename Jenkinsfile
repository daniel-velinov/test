pipeline {
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
          echo "Propertyfiles entered: ${propertyFile}"
		  sh "echo test > propertyFile.js"
		//  sh "echo '${propertyFile}' > propertyFile-$BUILD_NUMBER.js"
		 // sh "echo '${propertyFile}' > propertyFile-$BUILD_NUMBER.js"
		  // sh "cd /tmp && ansible-playbook -i hosts.ini test.yml --extra-vars 'count=${numContainers} build=$BUILD_NUMBER state=${reportState}'"
        }
      }
    }
  }
}