Jenkins Pipeline, özellikle yazılım geliştirme süreçlerinde kullanılan otomasyon araçlarının bir parçasıdır. Jenkins Pipeline, yazılım geliştirme süreçlerini otomatikleştirmek için kullanılan bir dizi adımı tanımlamaya ve yönetmeye olanak tanır. Bu adımlar, kod derleme, test etme, paketleme, dağıtma gibi işlemleri içerebilir.

``` groovy
def greet(name) {
    echo "Hello ${name}"
}

def multiplication(number) {
    return number * 2
}

pipeline {
    agent any
    
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: "", artifactNumToKeepStr: "", daysToKeepStr: "30", numToKeepStr: "2")
    }

    stages {
        stage("Calling functions") {
            steps {
                script {
                    greet("Jenkins")
                    def result = multiplication(5)
                    echo "output is ${result}"
                }
            }
        }
    }
}
