Upstream ve Downstream job'lar, Jenkins'te iş akışlarını (workflow) birbirine bağlamak için kullanılan kavramlardır. Bu kavramlar, bir işin (job) başka bir işi tetiklemesi veya bir işin başka bir işin sonucuna bağlı olarak çalışması durumlarını ifade eder.
Upstream job = Başka bir işi (downstream job) tetikleyen veya başlatan iştir.
Downstream job = Upstream job tarafından tetiklenen veya başlatılan iştir.

``` groovy
pipeline {
    agent any
    
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }

    stages {
        stage("Upstream job") {
            steps {
                echo "This is a upstream job"
            }
        }
        stage("Downstream job") {
            steps {
                build job: "pipeline-Jenkinsfile-7-b-downstream-job"
            }
        }
    }
}
