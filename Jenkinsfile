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

    	stage('Clone Github Repo') {
      		steps {
            	git branch: 'main', url: 'https://github.com/Horleryheancarh/php-todo.git'
      		}
    	}

		stage ('Build Docker Image') {
			steps {
				sh 'docker build -t yheancarh/php_todo:${BRANCH_NAME}-${BUILD_NUMBER} .'
			}
		}

		stage ('Push Image To Docker Hub') {
			steps {
				sh 'docker push yheancarh/php_todo:${BRANCH_NAME}-${BUILD_NUMBER}'
			}
		}

		stage('Cleanup') {
			steps {
				cleanWs(cleanWhenAborted: true, cleanWhenFailure: true, cleanWhenNotBuilt: true, cleanWhenUnstable: true, deleteDirs: true)

				sh 'docker system prune -f'
			}
		}
  	}
}