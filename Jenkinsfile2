pipeline {
  agent any
  stages {
    stage('compile') {
      steps {
        
          sh 'mvn clean compile -e'
        
      }
    }
    stage('test') {
      steps {
        
          sh 'mvn clean test -e'
        
      }
    }
    stage('jar') {
      steps {
          sh 'mvn clean package -e'
      }
    }
    stage('SonarQube') {
      steps {
        withSonarQubeEnv(installationName: 'sonar-local') { // You can override the credential to be used
          sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
        }
      }
    }
    stage('uploadNexus') {
      steps {
        nexusPublisher nexusInstanceId: 'nexus-roddy', nexusRepositoryId: 'test-nexus', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/Users/rafael/cursos-dev/diplomado-devops/ci-cd/ejemplo-maven/build/DevOpsUsach2020-0.0.1.jar']], mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '0.0.1']]]
      }
    }

  }
}