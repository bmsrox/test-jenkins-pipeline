pipeline {
    agent any
    stages {
        stage('Example Build') {
            steps {
                def server = getEnvironment().toLowerCase()
                echo server
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
