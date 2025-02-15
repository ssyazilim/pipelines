Jenkinsfile'daki tools bölümü, pipeline'ınızda kullanılacak araçların (tools) otomatik olarak yüklenmesini ve yapılandırılmasını sağlar. Bu bölüm, özellikle JDK, Maven, Gradle, Git gibi araçların pipeline boyunca kullanılabilir olmasını sağlamak için kullanılır. Jenkins, bu araçları otomatik olarak yükler ve ortam değişkenlerini (PATH gibi) ayarlar, böylece bu araçlara pipeline adımlarında kolayca erişebilirsiniz.

``` groovy
pipeline {
    agent any
    
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }

    tools {
        maven "Maven"
    }

    stages {
        stage("Checkout stage") {
            steps {
                checkout scmGit(branches: [[name: "*/master"]], extensions: [], userRemoteConfigs: [[url: "https://github.com/jenkins-docs/simple-java-maven-app.git"]])
            }
        }
        stage("Build project") {
            steps {
                echo "mvn compile"
            }
        }
    }
}
