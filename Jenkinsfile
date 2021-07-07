pipeline {
   agent any
	stages {
      stage('Git Checkout') {
         steps {
            git 'https://github.com/khann-adill/parking_backend.git'
		}
	}
	stage('Build') {
		steps {
				sh 'mvn clean verify -Dmaven.test.skip=true'
			}
		}
	}
	stage ('Release') {
		steps {
			sh 'export JENKINS_NODE_COOKIE=dontkillme ;nohup java -jar $WORKSPACE/target/*.jar &'
		}
	}
}
}
