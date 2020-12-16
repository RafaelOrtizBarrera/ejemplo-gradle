pipeline {
    agent any
    parameters { choice(name: 'TIPO_PIPELINE', choices: ['maven', 'gradle'], description: 'Determina con que herramienta se va a compilar') }
    
    stages {
        stage('Pipeline') {
            steps {
                script {
                  def script =  (params.TIPO_PIPELINE == 'maven') ? 'maven.groovy' :  'gradle.groovy';
                  echo 'pipeline seleccionado ' + script;
                  def tipoPipeline = load script;
                  tipoPipeline.call();
                }
            }
        }
    }
}
