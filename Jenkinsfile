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
                    sh 'nohup gradle bootRun &'
                  }
                  stage('test api'){
                    echo 'Esperando a que inicie el servidor'
                    sleep(time: 10, unit: "SECONDS")
                    script {
                      final String url = "http://localhost:8082/rest/mscovid/test?msg=testing"
                      final String response = sh(script: "curl -X GET $url", returnStdout: true).trim()

                      echo response
                    }
                  }
                  stage('nexus'){
                    nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'test-nexus-rafa', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/Users/rafael/cursos-dev/diplomado-devops/ci-cd/ejemplo-maven/build/DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.1']]]
                  }
                }
            }
        }
    }
}
