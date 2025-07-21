pipeline {
  agent {
    label 'NamitaNode'
  }

  stages {
        stage('build') {
        steps {
                bat 'mvn clean package'
        }
        post {
            success {
            archiveArtifacts artifacts: '**/*.xml',
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
