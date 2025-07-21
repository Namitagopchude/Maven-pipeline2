pipeline {
  agent {
    label 'NamitaNode'
  }

  tools{
      maven 'apache-maven-3.9.9'
  }

  stages {
        stage('build') {
        steps {
            bat 'mvn clean package -Denforcer.skip=true'
        }
        post {
            success {
               archiveArtifacts artifacts: '**/target/*.jar'
            }
        }
        }

        // stage('test') {
        //   steps {
            
        //     // One or more steps need to be included within the steps block.
        //   }
        
        // }

        // stage('deploy') {
        //   steps {
        //     // One or more steps need to be included within the steps block.
        //   }
        // }
    }
}
