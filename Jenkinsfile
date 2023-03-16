pipeline {
  agent { node { label 'ubuntu' } }
  stages { 
      stage ('git') {
        steps { 
          git url: 'https://github.com/spring-projects/spring-petclinic.git',
          branch: 'develop'
      }
      }
      stage ('build') { 
        steps {  
          sh './mvnw package'
      }
    }
      stage ('download the package') { 
        steps { 
          sh 'sudo cp ${WORKSPACE}/target/spring-petclinic-3.0.0-SNAPSHOT.jar /tmp/archive'
          }
    }
      stage ('upload to s3') { 
        steps { 
          sh 'aws s3 cp /tmp/archive/spring-petclinic-3.0.0-SNAPSHOT.jar s3://springpetclinic16feb/target/'
        }
      }
    }
}
