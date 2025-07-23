pipeline {
   agent { label 'NamitaNode' }

  tools{
      maven 'apache-maven-3.9.9'
      SonarQube Scanner 'SonarQube_Scanner1.7'
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
                     tools{ maven 'Ayushi-maven'}
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
        stage('SonarQube Analysis') {

            environment {
             SONAR_URL = "http://172.27.59.58:9000"
            }

            steps {
              withCredentials([string(credentialsId: 'Namita_Sonar', variable: 'Namita_Sonar')]) {
                bat 'mvn sonar:sonar -Dsonar.login=$Namita_Sonar -Dsonar.host.url=${SONAR_URL}'
              }
            }
            
        }

        stage('deploy') {

            when { expression {params.select_environments =='Test'} 
            beforeAgent true } 
    
            agent { label 'NamitaNode'}
            steps {
               
                bat 'java -jar "%WORKSPACE%/target/my-app-1.0-SNAPSHOT.jar"'
                 
            }
        }
    }
}
