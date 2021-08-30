pipeline {
    agent any
    stages {
		stage('Checkout') {
				steps {
					  sh 'checkout scm'
				}
			}
		stage('Mvn Build'){
			steps {
				sh 'mvn clean package'
			}
			post {
				success {
					echo 'Now Archiving...'
					archiveArtifacts artifacts: '**/target/*.war'
				}
			}
		}
		stage('Deploy the artifacts'){
		   steps {
			deploy adapters: [tomcat8(credentialsId: 'tomcat', path: '', url: 'http://18.118.1.215:8081')], contextPath: null, war: '**/*.war'
		   }
	    }
    }
}
