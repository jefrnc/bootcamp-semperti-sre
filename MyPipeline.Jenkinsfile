pipeline {
    agent {
        node (){
            label 'bc-jfranco'
        }
    }
    environment {
		VERSION = "99.99"
    }

    stages {
			stage('Step 1 - Configuración') {
				steps {
					sh "sudo /opt/openvpn/connect-vpn.sh"
				}
			}
			stage('Step 2 - Unit testing') {
				steps {
					sh "echo TBD"
 					sh "mvn test -f Code/pom.xml"
				}
			}
			stage('Step 3 - Snapshot & Upload a Nexus') {
				steps {
                	sh 'ansible-playbook snapshot.yml --extra-vars "version=${VERSION}"'
				}
			}
			stage('Step 4 - Release & Upload a Nexus') {
				steps {
					sh 'ansible-playbook release.yml --extra-vars "version=${VERSION}"'
				}
			}
			stage('Step 5 - Creacion del Docker & Publicacion ') {
				steps {
					sh 'ansible-playbook docker-publish.yml --extra-vars "version=${VERSION}"'
				}
			}
			 
    }
}