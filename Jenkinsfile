node{
properties(
    [parameters([choice(choices: ["A", "B", "C"].join("\n"),
    description: 'Some choice parameter', 
    name: 'environment')])])
    
    switch(params.environment ){
        case 'A':
            echo "A will be processed"
            properties(
            [parameters([choice(choices: ["A1", "A2", "A3"].join("\n"),
            description: 'Some choice parameter2', 
            name: 'service')])])
            break
        case 'B':
            echo "B will be processed"
            break
        case 'C':
            echo "C will be processed"
            break
    }
}
