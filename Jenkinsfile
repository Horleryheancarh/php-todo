pipeline {
    agent any
	
	stages {
		stage("Initial cleanup") {
			steps {
				dir("${WORKSPACE}") {
					deleteDir()
				}
			}
		}

    	stage('Checkout SCM') {
      		steps {
            	git branch: 'main', url: 'https://github.com/Horleryheancarh/php-todo.git'
      		}
    	}

		stage ('Build Docker Image') {
			steps {
				sh 'docker build -t yheancarh/php_todo:${BRANCH_NAME}-${BUILD_NUMBER} ./php-todo/'
			}
		}

		stage ('Push Image To Docker Hub') {
			steps {
				sh 'docker login -u ${username} -p ${password}'

				sh 'docker push yheancarh/php_todo:${BRANCH_NAME}-${BUILD_NUMBER}'

				sh 'docker logout'
			}
		}

  	}
}