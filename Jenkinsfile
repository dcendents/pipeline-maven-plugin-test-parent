pipeline {
	agent any
	triggers { 
		snapshotDependencies()
	}
	stages {
		stage('Clone') {
			steps {
				checkout scm
			}
		}
		stage('Build') {
			steps {
				withMaven(
						maven: 'maven-latest',
						publisherStrategy: 'EXPLICIT',
						options: [
							dependenciesFingerprintPublisher(includeScopeTest: true), 
							pipelineGraphPublisher(includeScopeTest: true, lifecycleThreshold: 'install')
						]) {
					sh script: "mvn clean install"
				}
			}
		}
	}
}
