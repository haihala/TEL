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
                    sh "cargo fmt --all -- --check"
                }
            }
        }
        stage('Doc') {
            steps {
                dir('TEL') {
                    sh "cargo doc"
                }
            }
        }
    }
}