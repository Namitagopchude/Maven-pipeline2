pipeline {
  agent { label 'NamitaNode'}

  tools{
      maven 'apache-maven-3.9.9'
    }

  parameters {
    choice choices: ['Test ', 'Prod'], name: 'select_environments'
   }

  stages {
        stage('build') {
            steps {
                bat 'mvn clean package -Denforcer.skip=true -DskipTests=true'
            }
        
        }

        stage('test') {
          parallel {
                stage('testA')
                {
                    agent { label 'NamitaNode' }
                    steps{
                        echo "This is test A"
                        bat 'mvn test'
                    }
                    
                }

                stage('test B')
                {
                     agent { label 'ayushinode' }
                     steps{
                        echo "This is test B"
                        bat 'mvn test'
                    }
                }


            }
            post {
                success {
                archiveArtifacts artifacts: '**/target/*.jar'
                }
            }
        
        }

        stage('deploy') {
            
            when{
                    expression {params.select_environments == Test}
                    beforeAgent true
                    agent { label 'NamitaNode'}
                }

            steps {

                bat 'java -jar "%WORKSPACE%/target/my-app-1.0-SNAPSHOT.jar"'
                 
            }
        }
    }
}
