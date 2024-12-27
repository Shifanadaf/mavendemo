pipeline{
  agent any
  tools{
    maven 'sonarmaven'
  }
  environment{
    JAVA_PATH="C:\\Program Files\\Java\\jdk-17\\bin"
  }
  stages{
    stage('Checkout Code') {
            steps {
                checkout scm
            }
    }
    stage('Build'){
      steps{
     // Adjust if the POM is in a subdirectory
        
            bat 'mvn clean package'
        }
    }
     
    stage('SonarQube Analysis'){
   environment{
       SONAR_TOKEN=credentials('sonarqube-token')
       MAVEN_HOME="C:\\Program Files\\apache-maven-3.9.9\\bin" // Adjust this path
       PATH="${env.PATH};${env.MAVEN_HOME}\\bin"
   }
   steps{
       bat '''
       set PATH=%JAVA_PATH%;
       set PATH=%MAVEN_HOME%\\bin;%PATH%;
       cd my-app
       mvn clean verify sonar:sonar -Dsonar.projectKey=mavendemo -Dsonar.projectName='mavendemo' -Dsonar.source=my-app -Dsonar.host.url=http://localhost:9000 -Dsonar.token=${SONAR_TOKEN}
       '''
   }
  }
  }
  post{
    success{
      echo "DONE SUCCESSFULLY"
    }
    failure{
      echo "WRONG"
    }
  }
  
}
