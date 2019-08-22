/*node{
properties(
    [parameters([choice(choices: ["A", "B", "C"].join("\n"),
    description: 'Some choice parameter', 
    name: 'environment')])])
    
    switch(params.environment ){
        case 'A':
            echo "A will be processed"
            break
        case 'B':
            echo "B will be processed"
            break
        case 'C':
            echo "C will be processed"
            break
    }
}

node{
    def choice1
    def choice2

    stage ('Select'){
        choice1 = input( id: 'userInput', message: 'Select your choice', parameters: [ [$class: 'ChoiceParameterDefinition', choices: 'aa\nbb', description: '', name: ''] ])
        if(choice1.equals("aa")){
            choice2 = input( id: 'userInput', message: 'Select your choice', parameters: [ [$class: 'ChoiceParameterDefinition', choices: 'yy\nww', description: '', name: ''] ])
        }else{
            choice2 = input( id: 'userInput', message: 'Select your choice', parameters: [ [$class: 'ChoiceParameterDefinition', choices: 'gg\nkk', description: '', name: ''] ])
        }
    }
}


parameters {
        activeChoiceParam('States') {
            description('Select a state option')
            filterable()
            choiceType('SINGLE_SELECT')
            groovyScript {
                script('["Sao Paulo", "Rio de Janeiro", "Parana:selected", "Acre"]')
                fallbackScript('return ["ERROR"]')
            }
        }
        activeChoiceReactiveParam('Cities') {
            description('Active Choices Reactive parameter')
            filterable()
            choiceType('CHECKBOX')
            groovyScript {
                script('''
                        if (States.equals('Sao Paulo')) {
                            return ['Barretos', 'Sao Paulo', 'Itu'];
                        } else if (States.equals('Rio de Janeiro')) {
                            return ['Rio de Janeiro', 'Mangaratiba']
                        } else if (States.equals('Parana')) {
                            return ['Curitiba', 'Ponta Grossa']
                        } else if (States.equals('Acre')) {
                            return ['Rio Branco', 'Acrelandia']
                        } else {
                            return ['Unknown state']
                        }
                                               ''')
                fallbackScript('return ["Script error!"]')
            }
            referencedParameter('States')
        }
    }


node {
       
properties(
[
        [
                $class              : 'ParametersDefinitionProperty',
                        parameterDefinitions: [
                        [
                                $class     : 'ChoiceParameterDefinition',
                                choices    : 'aaa\nbbb',
                                description: 'select your choice : ',
                                name       : 'choice1'
                        ],
                        [
                                $class     : 'ChoiceParameterDefinition',
                                choices    : 'ccc\nddd',
                                description: 'select another choice : ',
                                name       : 'choice2'
                        ],
                          [
                                $class     : 'ChoiceParameterDefinition',
                                choices    : 'eee\nfff',
                                description: 'select another choice : ',
                                name       : 'choice2'
                        ]
]]])
}
*/

properties([
    parameters([
        [$class: 'ChoiceParameterDefinition', 
            choiceType: 'PT_SINGLE_SELECT', 
            description: 'Select the Env Name from the Dropdown List', 
            filterLength: 1, 
            filterable: true, 
            name: 'Env', 
            randomName: 'choice-parameter-5631314439613978', 
            script: [
                $class: 'GroovyScript', 
                fallbackScript: [
                    classpath: [], 
                    sandbox: false, 
                    script: 
                        'return[\'Could not get Env\']'
                ], 
                script: [
                    classpath: [], 
                    sandbox: false, 
                    script: 
                        'return["Dev","QA","Stage","Prod"]'
                ]
            ]
        ], 
        [$class: 'CascadeDynamicChoiceParameter', 
            choiceType: 'PT_SINGLE_SELECT', 
            description: 'Select the Server from the Dropdown List', 
            filterLength: 1, 
            filterable: true, 
            name: 'Server', 
            randomName: 'choice-parameter-5631314456178619', 
            referencedParameters: 'Env', 
            script: [
                $class: 'GroovyScript', 
                fallbackScript: [
                    classpath: [], 
                    sandbox: false, 
                    script: 
                        'return[\'Could not get Environment from Env Param\']'
                ], 
                script: [
                    classpath: [], 
                    sandbox: false, 
                    script: 
                        ''' if (Env.equals("Dev")){
                                return["devaaa001","devaaa002","devbbb001","devbbb002","devccc001","devccc002"]
                            }
                            else if(Env.equals("QA")){
                                return["qaaaa001","qabbb002","qaccc003"]
                            }
                            else if(Env.equals("Stage")){
                                return["staaa001","stbbb002","stccc003"]
                            }
                            else if(Env.equals("Prod")){
                                return["praaa001","prbbb002","prccc003"]
                            }
                        '''
                ]
            ]
        ]
    ])
])

pipeline {
  environment {
         vari = ""
  }
  agent any
  stages {
      stage ("Example") {
        steps {
         script{
          echo 'Hello'
          echo "${params.Env}"
          echo "${params.Server}"
          if (params.Server.equals("Could not get Environment from Env Param")) {
              echo "Must be the first build after Pipeline deployment.  Aborting the build"
              currentBuild.result = 'ABORTED'
              return
          }
          echo "Crossed param validation"
        } }
      }
  }
}

