pipeline {
    agent any 
      environment {
      SPRING_VER = "0.0.1-SNAPSHOT"
     }

    tools {
        maven "MAVEN3"
	jdk   "jdk11"
    }

    stages {
        stage('Initialize'){
            steps{
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = /opt/apache-maven-3.8.3"
            }
        }
	//stage('Validate') {
	//      steps {
	//          sh 'mvn validate'
	//          }
	//      }
	
        stage('Build') {
            steps {
                sh 'mvn -pl ${SPRING_MOD}  clean'
                sh 'mvn -pl ${SPRING_MOD} package -Dmaven.test.skip'
            }
        }

        stage('Deploy') {
            steps {
		sh 'ansible-galaxy collection install kubernetes.core -p ./ansible/collections'
		sh 'ansible-playbook ansible/deploy.yml -i ansible/roles/deploy/tests/inventory -e "version=${SPRING_VER}" -e "workdir=${WORKSPACE}" -e "module=${SPRING_MOD}"'
		
	}	
	}
     }
  //  post {
  //      always {
  //         junit(
  //       allowEmptyResults: true,
  //     testResults: '*/test-reports/.xml'
  //  )
  // }
  // } 
}
