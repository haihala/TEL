pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                dir('TEL') {
                    sh "cargo build"
                }
            }
        }
        stage('Test') {
            steps {
                dir('TEL') {
                    sh "cargo test"
                }
            }
        }
        stage('Clippy') {
            steps {
                dir('TEL') {
                    sh "cargo clippy --all"
                }
            }
        }
        stage('Rustfmt') {
            steps {
                // The build will fail if rustfmt thinks any changes are
                // required.
                dir('TEL') {
                    sh "cargo fmt --all -- --write-mode diff"
                }
            }
        }
        stage('Doc') {
            steps {
                dir('TEL') {
                    sh "cargo doc"
                    // We run a python `SimpleHTTPServer` against
                    // /var/lib/jenkins/jobs/<repo>/branches/master/javadoc to
                    // display our docs
                    step([$class: 'JavadocArchiver',
                        javadocDir: 'target/doc',
                        keepAll: false])
                }
            }
        }
    }
}