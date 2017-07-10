node {
    try {
        stage("Checkout") {
           checkout scm
        }
        stage("test") {
           echo "Testing"
        }
        
        stage("Approve") {
            input 'Want deploy?'
        }
        
        stage("deploy") {
            echo "Deploy"
        }
        
        stage("Changelog") {
            echo currentBuild.changeSets
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

    def enviroment = getEnvironment()
    status = status ?: 'SUCCESS'

    if (status == 'SUCCESS') {
        message = "A new software version has been released in '${enviroment}'"
    } else {
        message = "Something went wrong on project build! Please check it. '${env.BUILD_URL}'"
    }

    sendEmail(message, status)
}

def getChangeString() {
    MAX_MSG_LEN = 100
    def changeString = ""

    echo "Gathering SCM changes"
    def changeLogSets = currentBuild.rawBuild.changeSets
    for (int i = 0; i < changeLogSets.size(); i++) {
        def entries = changeLogSets[i].items
        for (int j = 0; j < entries.length; j++) {
            def entry = entries[j]
            truncated_msg = entry.msg.take(MAX_MSG_LEN)
            changeString += " - ${truncated_msg} [${entry.author}]\n"
        }
    }

    if (!changeString) {
        changeString = " - No new changes"
    }
    return changeString
}

def sendEmail(String message, String statusName) {
    mail (
        to: "bms_sp@hotmail.com",
        cc: "bmsrox@gmail.com",
        subject: "${statusName}: Job '${env.JOB_NAME}' [${env.BUILD_NUMBER}]",
        mimeType: 'text/html',
        body: message
    );
}
