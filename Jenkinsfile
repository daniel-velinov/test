pipeline {
  parameters {
    choice(name: 'numContainers', choices: ['1', '2', '3', '4', '5'], description: 'Enter number of containers needed')
    choice(name: 'reportState', choices: ['new', 'update'], description: 'Enter whether new or update report')
	choice(name: 'propertyFile', text: '''
									sample 
									text
									''', description: 'Enter the properties file as raw text')
  }

 stages {
  stage('Run cypress containers on Dione') {
    steps {
      script {
          echo "Selected number of containers: ${numContainers}"
          echo "Report selected: ${reportState}"
          echo "Propertyfiles entered: ${propertyFile}"
        }
      }
    }
  }
}