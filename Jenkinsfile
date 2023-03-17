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
    stage ('sonarqube') {
        steps {
          withSonarQubeEnv('Kiranteja623') {
                    sh 'mvn clean package sonar:sonar -Dsonar.organization=kiranteja623 -Dsonar.login=ddfb007e5e67490bc157bd464d92bdfd2690f1d2 -Dsonar.host.url=https://sonarcloud.io -Dsonar.projectKey=kiranteja623/petclinic'
                }
        }
  }
      stage ('download the package') { 
        steps { 
          sh 'sudo cp ${WORKSPACE}/target/spring-petclinic-3.0.0-SNAPSHOT.jar /tmp/archive'
          }
    }
    stage ('deploy the package using ansible') {
      steps {
        sh 'ansible-playbook -i host  spc.yaml'
      }
    }
}
}
