Jenkinsfile'da döngüler (loops), Groovy dilinin sunduğu esneklik sayesinde pipeline'larınızda tekrarlayan işlemleri otomatikleştirmek için kullanılır. Döngüler, özellikle birden fazla adımı tekrarlamanız gereken durumlarda (örneğin, birden fazla ortamda deploy işlemi yapmak veya birden fazla modülü test etmek) oldukça kullanışlıdır.

``` groovy
pipeline {
    agent any
    
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }

    stages {
        stage("Loop usage") {
            steps {
                script {
                    echo "Table of 5"
                    for (int i=1; i <= 10; i++) {
                        echo "5 x ${i} = ${5 * i}"
                    }
                }
            }
        }
    }
}
