pipeline {
    agent any

    environment {
        CODE_DIRECTORY = 'task-event-log'
    }

    stages {
        stage('Build') {
            steps {
                dir('${CODE_DIRECTORY}') {
                    sh "cargo build"
                }
            }
        }
        stage('Test') {
            steps {
                dir('${CODE_DIRECTORY}') {
                    sh "cargo test"
                }
            }
        }
        stage('Clippy') {
            steps {
                dir('${CODE_DIRECTORY}') {
                    sh "cargo clippy --all -- -D warnings"
                }
            }
        }
        stage('Rustfmt') {
            steps {
                // The build will fail if rustfmt thinks any changes are
                // required.
                dir('${CODE_DIRECTORY}') {
                    sh "cargo fmt --all -- --check"
                }
            }
        }
        stage('Doc') {
            steps {
                dir('${CODE_DIRECTORY}') {
                    sh "cargo doc"
                }
            }
        }
    }
}