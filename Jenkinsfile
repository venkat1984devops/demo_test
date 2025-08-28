pipeline {
     agent any
  
    options {
        timeout(time: 1, unit: 'HOURS') 
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('SCM') {
            steps {
                git url: 'https://github.com/spring-projects/spring-petclinic.git',
                    branch: 'main'
            }
        }
	stage('build with sonar') {
		steps {
			withSonarQubeEnv(credentialsId: 'SONAR_TOKEN', installationName: 'SONAR_CLOUD') { // You can override the credential to be used
				sh '/opt/maven/bin/mvn clean package org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar -D sonar.organization=Jenkins_CICD_Testing
 -D sonar.projectKey=e7ab73258a2d8e13a4fce6a3d5e272dbda4702de'
			}
			junit testResults: '**/surefire-reports/*.xml'
			archive '**/target/spring-petclinic-*.jar'
		}
	}
	stage("Quality Gate") {
		steps {
			timeout(time: 1, unit: 'HOURS') {
				// Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
				// true = set pipeline to UNSTABLE, false = don't
				waitForQualityGate abortPipeline: true
			}
		}
	}
	
  }
    
}
