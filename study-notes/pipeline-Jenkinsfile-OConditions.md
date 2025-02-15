``` groovy
pipeline {
    agent any

    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }

    stages {
        stage("Script usage") {
            steps {
                script {
                    def age = 40
                    if (age >= 18) {
                        echo "You are eligible to vote"
                    }
                    else {
                        echo "You are not eligible to vote"    
                    }
                }
            }
        }
    }
}