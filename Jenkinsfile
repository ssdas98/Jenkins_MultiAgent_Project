pipeline {
    agent none
    stages {
        stage('Matrix Build') {
            matrix {
                axes {
                    axis {
                        name 'OS'
                        values 'linux', 'windows', 'mac'
                    }
                    axis {
                        name 'JDK'
                        values 'openjdk8', 'openjdk11'
                    }
                }
                stages {
                    stage('Build') {
                        agent { 
                            label "${OS}-${JDK}"
                        }
                        steps {
                            echo "Building on ${OS} with ${JDK}..."
                            // Your build steps here
                        }
                    }
                    stage('Test') {
                        agent {
                            label "${OS}-${JDK}"
                        }
                        steps {
                            echo "Running tests on ${OS} with ${JDK}..."
                            // Your test steps here
                        }
                    }
                }
            }
        }
    }
}
