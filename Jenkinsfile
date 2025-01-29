pipeline {
    agent none
    stages {
        stage('Build matrix') {
            matrix {
                axes {
                    axis {
                        name "OS"
                        values "linux", "windows", "mac"
                    }
                    axis {
                        name "JDK"
                        values "openjdk8", "openjdk11"
                    }
                }
            }
        }
    stages {
        stage('Build') {
            agent {
                label "${OS}-${JDK}"
            }
            steps {
                echo "Building on ${OS} with ${JDK}"
            }
        }
        stage('Test') {
            agent {
                label "${OS}-${JDK}"
            }
            steps {
                echo "Testng on ${OS} with ${JDK}"
            }
        }
    }
}
}
