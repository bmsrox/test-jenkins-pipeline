pipeline {
    agent any
    stages {
        stage('Example Build') {
            steps {
                def myStr = "mystring"
                myStr = "\u\L" + myStr      
                println myStr
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
