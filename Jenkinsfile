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
		steps {
		     sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dmaven.test.skip=true -Dsonar.host.url=https://sonarcloud.io -Dsonar.projectKey=khann-adill_parking_backend -Dsonar.organization=khann-adill -Dsonar.login=7aa74d987bec902768be8aad1518179de9cff4fa'
		}	
		}
	stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
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
