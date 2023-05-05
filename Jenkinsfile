pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/akhilvijay15/CICD_project2.git'
                }
            }
        }
     stage('Build'){
          steps{
             sh 'mvn install -DskipTests'
          }
          post {
             success {
                  echo 'Now Archiving it...'
                  archiveArtifacts artifacts: '**/target/*.jar,.war'
             }
          }
       }
       stage('UNIT TEST'){
          steps{
             sh 'mvn test'
          }
        }
        stage('CheckStyle Analysis'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
         stage('Sonar Analysis'){
            environment{
                     scannerHome = tool 'sonar4.8'
            }

         steps {
            withSonarQubeEnv('sonar') {
               sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=cicd_project2 \
                   -Dsonar.projectName=cicd_project2 \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
            }
         }
      }

    }

}         