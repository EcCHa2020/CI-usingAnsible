pipeline {
    agent any
    
    tools
    {
       maven "Maven_3.6.3"
    }
     
    stages {
        	stage('checkout') {
			steps {
				git branch: 'development', url: 'https://github.com/EcCHa2020/CI-usingAnsible.git'
	   		}
        	}
        	stage('Tools Init') {
			steps {
                		script {
                    			echo "PATH = ${PATH}"
                    			echo "MVN_HOME = ${MVN_HOME}"
					def tfHome = tool name: 'Ansible'
					env.PATH = "${tfHome}:${env.PATH}"
					sh 'ansible --version'
                		}
            		}
        	}
        	stage('Execute Maven') {
            		steps {
				sh 'mvn package'             
			}
        	}
		stage('Ansible Deploy') {
            		steps {
				sh "ansible-playbook main.yml -i inventories/dev/hosts -- user jenkins --key-file ~/.ssh/id_rsa"
			}
		}
	}
}
