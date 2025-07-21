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
            bat 'mvn clean package'
        }
        post {
            success {
               archiveArtifacts artifacts: '**/target/*.war'
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
