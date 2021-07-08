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
	stage('Code Analysis') {
		  environment { 
                    SONAR_TOKEN = 7aa74d987bec902768be8aad1518179de9cff4fa
                }
		steps {
				sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dmaven.test.skip=true'
		}	
		}
	stage ('Release') {
		when {
		branch 'master'
		}
		steps {
			sh 'export JENKINS_NODE_COOKIE=dontkillme ;nohup java -jar $WORKSPACE/target/*.jar &'
		}
	}
}
}
