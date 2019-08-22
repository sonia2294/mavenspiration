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

node{
    parameters {
        choice(name: 'DataCenter', choices:'Foo\nBar')
        choice(name: 'AvailabilityZone', choices: if(DataCenter.equals("Foo") {return 'A\nB'} else {return 'C\nD'}))
    }
}

