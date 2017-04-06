pipeline {
    agent any
    stages {
        stage('Example Build') {
            steps {
                def a1 = ["please", "spare", "my", "aching", "fingers"]
                // Current:
                def a2 =  a1.collect { it[0].toUpperCase() + it.substring(1)  }    // Ugh!   This is every bit as clunky as java -- it's awful.

                // Desired:
                def a2 =  a1.collect { "\u$it" }                                   // NOTE:   the \u would have saved me 30 characters of typing!!!

                a2.each { println "--> $it <--" }
            }
        }
    }
}
