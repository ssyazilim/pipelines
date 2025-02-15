Jenkinsfile içerisinde parameters alanı, pipeline'ın çalıştırılmadan önce kullanıcı tarafından belirlenebilen parametreleri tanımlamak için kullanılır. Bu parametreler, pipeline'ın davranışını özelleştirmek veya farklı senaryolara uyum sağlamak için kullanılabilir. parameters alanı, pipeline'ın başında tanımlanır ve bu parametreler Jenkins UI üzerinden kullanıcıya sunulur.

``` groovy
pipeline {
    agent any

    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }

    parameters {
        string defaultValue: "Erol", name: "FIRSTNAME"
        booleanParam defaultValue: true, name: "IS_USER"
    }

    stages {
        stage("Parameters job") {
            steps {
                echo "My name is $params.FIRSTNAME. My boolean value is => ($params.IS_USER)"
            }
        }
    }
}
