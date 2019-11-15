node('') {
	stage('Poll') {
		checkout scm
	}
	stage('Build & Unit test'){
		withMaven(maven:'mm'){
			bat 'mvn clean verify -DskipITs=true';}
		junit '**/target/surefire-reports/TEST-*.xml'
		archive 'target/*.jar'
	}
	stage('Static Code Analysis'){
		withMaven(maven:'mm'){
			bat 'mvn clean verify sonar:sonar -Dsonar.projectName=exemple-sonar -Dsonar.projectKey=exemple-sonar -Dsonar.projectVersion=$BUILD_NUMBER';
		}
	}
	stage ('Integration Test'){
		withMaven(maven:'mm'){
			bat 'mvn clean verify -Dsurefire.skip=true';}
		junit '**/target/failsafe-reports/TEST-*.xml'
		archive 'target/*.jar'
	}
	
}
