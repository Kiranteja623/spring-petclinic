pipeline {
  agent { node { label 'ubuntu' } }
  stages { 
      stage ('git') {
        steps { 
          git url: 'https://github.com/spring-projects/spring-petclinic.git',
          branch: 'main'
      }
      }
      stage ('build') { 
        steps {  
          sh './mvnw package'
      }
    }
      stage ('download the package') { 
        steps { 
          sh 'sudo cp ${WORKSPACE}/target/spring-petclinic-3.0.0-SNAPSHOT.jar /home/ubuntu/spc'
          }
    }
      stage ('deployment') { 
        steps { 
          sh 'ansible-playbook -i host spc-playbook.yaml'
        }
      }
    }
}
























