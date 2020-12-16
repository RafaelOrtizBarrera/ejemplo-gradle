pipeline {
    agent any
    parameters { choice(name: 'TIPO_PIPELINE', choices: ['maven', 'gradle'], description: 'Determina con que herramienta se va a compilar') }
    
    stages {
        stage('Pipeline') {
            steps {
                script {
                  def tipoPipeline =  (params.TIPO_PIPELINE == 'maven') ? load 'maven.groovy' : load 'gradle.groovy';
                  tipoPipeline.call();
                }
            }
        }
    }
}
