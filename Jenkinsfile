pipeline {
  agent { node { label 'ubuntu' } }
  triggers { pollSCM('* * * * *') }
  stages {
    stage ('git') {
      steps {
      git url: 'https://github.com/Kiranteja623/spring-petclinic.git',
          branch: 'release'
    }
    }
    stage ('package') {
      steps {
          sh 'mvn package'
    }
    }
      stage ('download the package') { 
        steps { 
          sh 'sudo cp ${WORKSPACE}/target/spring-petclinic-3.0.0-SNAPSHOT.jar /tmp/archive'
          }
    }
    stage ('deploy the package using ansible') {
      agent { node { label 'master' } }
      steps {
        sh 'ansible -i hosts -m ping all'
      }
    }
}
}
