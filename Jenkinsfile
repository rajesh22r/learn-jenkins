pipeline {
    agent {
        label 'AGENT-1'
    
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    options{
        timeout( time: 10, unit: 'MINUTES')
        disableConcurrentBuilds()
    }
    stages {
        stage('Build') { 
            steps {
              sh  'echo this is build'
              sh 'sleep 10'
            }
        }
        stage('Test') { 
            steps {
               sh   'echo this is test'
               sh 'echo test again'
            }
        }
        stage('Deploy') { 
            when{
                branch 'production'
            }
            steps {
                sh 'echo this is deploy'
                
            }
        }
        stage('print params') { 
            steps {
                echo " Hello ${params.PERSON}"
                echo " biography: ${params.BIOGRAPHY}"
                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Password: ${params.PASSWORD}"
                
            }
        }
         
         
        stage('Approval') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo "Hello, ${PERSON}, nice to meet you."
            }
        }
    
    }
        post { 
        always { 
            deleteDir()
        }
        success{
             
             echo 'this section runs when pipeline success'
         }
        failure{
             echo 'this section runs when pipeline failure'
        }
    }

}