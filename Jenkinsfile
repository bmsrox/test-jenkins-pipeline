node(){
    def env = getEnvironment()
    
    stage("Test 1") {
        echo env
    }
    stage("Test 2") {
        echo env.toLowerCase()
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
