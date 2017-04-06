pipeline {
    agent any
    stages {
        stage('Example Build') {
            def server = getEnvironment().toLowerCase()
            steps {
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
