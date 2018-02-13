// Tell Jenkins how to build projects from this repository
pipeline {
	agent {
		label 'magicdraw19'
	} 

	// Keep only the last 5 builds
	options {
		buildDiscarder(logRotator(numToKeepStr: '5'))
	}
	
	tools { 
		maven 'Maven 3.3.9' 
		jdk 'Oracle JDK 8' 
	}

	stages { 
		stage('Build Plug-in') { 
			steps {
				configFileProvider([configFile(fileId: 'default-maven-settings', variable: 'MAVEN_SETTINGS')]) {
					sh 'mvn clean install -Dmd.home=$MD19_HOME -s $MAVEN_SETTINGS'
				}
			}
		}
	}

	post {
		always {
			sh 'rm v4md.zip'
			zip archive: true, dir: 'com.incquerylabs.v4md/target/plugin-release', glob: '', zipFile: 'v4md.zip'
		}
	}
}