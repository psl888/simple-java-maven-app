pipeline {
   //代理
    agent {
        docker {		
            image 'maven' 
            args '-v /root/.m2:/root/.m2' 			
        }
    }
    stages {
	//构建
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
	//test
		stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
				//归档JUnit XML报告
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
		stage('Deliver') {
				steps {
					sh './jenkins/scripts/deliver.sh'
				}
			}
    }
}

