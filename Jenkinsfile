node {
    try {
        
        environment = getEnvironment()
        
        stage("Checkout") {
           checkout scm
        }
        stage("test") {
           echo "${GIT_COMMIT}"
        }
        stage("deploy") {
            echo "Deploy to ${environment}"
        }
    } catch (e) {
        currentBuild.result = "FAILED"
        throw e
    } finally {
        notifyStatus(currentBuild.result)
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

def notifyStatus(String status) {
    status = status ?: 'SUCCESS'

    if (status == 'SUCCESS') {
        message = "A new software version has been released in '${environment}'"
    } else {
        message = "Something went wrong on project build! Please check it. '${env.BUILD_URL}'"
    }

    sendEmail(message, status)
}

def sendEmail(String message, String statusName) {
    mail (
        to: "bmsrox@gmail.com, bms_sp@hotmail.com",
        subject: "${statusName}: Job '${env.JOB_NAME}' [${env.BUILD_NUMBER}]",
        mimeType: 'text/html',
        body: message
    );
}
