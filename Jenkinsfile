properties([
  [$class: 'ParametersDefinitionProperty', parameterDefinitions: [
    [$class: 'StringParameterDefinition',
      name: 'Greeting',
      defaultValue: 'Hello',
      description: 'How should I greet the world?']
  ]]
])
node('builder') {  
    stage('Preparation') { 
        echo "{params.Greeting} World!" 
    }
    stage('Repo Sync') { 
        // 
    }
    stage('Build Process') { 
        // 
    }
    stage('OTA Package') {
        //
    }
    stage('Archiving') {
        //
    }
    stage('Publishing') {
        //
    }
}
