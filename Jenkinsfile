pipeline {
    agent any

    stages {
        stage('Pipeline') {
            steps {
                script {
                  stage('build & test') {
                    sh 'gradle clean build'
                  }
                  stage('sonar'){
                    // corresponde a lo que se configuro en gloabal tool configuration
                    def scannerHome = tool 'sonar';
                    // nombre en configuraciones generales
                    withSonarQubeEnv('sonar-local') { 
                      sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-gradle -Dsonar.java.binaries=build"
                    }
                  }
                  stage('run'){

                  }
                  stage('test api'){

                  }
                  stage('nexus'){

                  }
                }
            }
        }
    }
}
