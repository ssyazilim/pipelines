Checkout, yazılım geliştirme süreçlerinde, özellikle versiyon kontrol sistemlerinde (VCS) kullanılan bir terimdir. Temel olarak, bir kaynak kod deposundan (repository) belirli bir versiyonu veya branch'i yerel bir ortama indirme işlemidir. Jenkins gibi CI/CD araçlarında da checkout, genellikle bir Git veya diğer SCM (Source Code Management) depolarından kodu almak için kullanılır.

``` groovy
pipeline {
    agent any
    
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }

    stages {
        stage("Checkout stage") {
            steps {
                checkout scmGit(branches: [[name: "*/master"]], extensions: [], userRemoteConfigs: [[url: "https://github.com/jenkins-docs/simple-java-maven-app.git"]])
            }
        }
        stage("Contents") {
            steps {
                sh "ls -all"
            }
        }
    }
}
