pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World ttt33"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
    }
}
