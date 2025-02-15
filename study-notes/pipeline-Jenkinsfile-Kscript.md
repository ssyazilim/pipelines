Script, bilgisayar biliminde ve yazılım geliştirmede, belirli bir görevi otomatikleştirmek veya gerçekleştirmek için yazılan komut dizileridir. Script'ler, genellikle yorumlanan (interpreted) dillerde yazılır ve bir işletim sistemi, uygulama veya platform tarafından doğrudan çalıştırılabilir. Script'ler, tekrarlayan görevleri otomatikleştirmek, sistem yönetimini kolaylaştırmak veya karmaşık işlemleri basitleştirmek için kullanılır.

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
                    def age = 5
                    def result = age * 2
                    echo "Hello my age is ${result}"
                }
            }
        }
    }
}
