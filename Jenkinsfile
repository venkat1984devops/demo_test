pipeline {
    agent any 
    tools {
        maven 'maven3' 
    }
    stages {
        stage('SCM') {
            steps {
                git url: 'https://github.com/spring-projects/spring-petclinic.git', 
                    branch: 'main'
            }
            
        }
        stage('BUILD') {
            steps {
                sh 'mvn --version'
                sh 'mvn validate'
                
            }
            
        }
    }
}
