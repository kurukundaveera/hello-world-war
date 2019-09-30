pipeline {
    agent any
    stages {
        stage('Checkout') {
         	   steps {
               		git 'https://github.com/kurukundaveera/hello-world-war.git'
            }
        }
		
		stage('Build') {
         	   steps {
               		sh "/opt/maven/bin/mvn clean deploy sonar:sonar"
            }
		}
		
		stage('Deploy') {
         	   steps {
               		deploy adapters: [tomcat8(credentialsId: 'tomcat', path: '', url: 'http://13.233.200.92:8888/')], contextPath: 'HelloWorld', war: '**/*.war'

            }
		}
		
    }
	
}

