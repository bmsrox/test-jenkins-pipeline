pipeline {
    agent any
    parameters {
        string(name: 'ENV', defaultValue: getEnvironment())
    }
    stages {
        stage ("Checkout") {
            
        }
        stage('Example Build') {
            steps {
                echo ${params.ENV}
            }
        }
    }
}

def getEnvironment() {
    def branch = "${env.BRANCH_NAME}"
    if (branch == "master") {
        return "Production"
    } else if (branch == "staging") {
        return "Staging"
    } else {
        return "Development"
    }
}
