pipeline {
  agent any
  parameters {
    choice(name: 'numContainers', choices: ['1', '2', '3', '4', '5'], description: 'Enter number of containers needed')
    choice(name: 'reportState', choices: ['new', 'update'], description: 'Enter whether new or update report')
//	string(name: 'propertyFile', defaultValue: 'default', description: 'Enter Propertyfiles as raw text')
	text(name: 'propertyFile-text', defaultValue: 'One\nTwo\nThree\n', description: 'Enter Propertyfiles as raw text')
  }

 stages {
  stage('Run cypress containers on Dione') {
    steps {
      script {
          echo "Selected number of containers: ${numContainers}"
          echo "Report selected: ${reportState}"
          echo "Propertyfiles entered: ${propertyFile-text}"
        }
      }
    }
  }
}