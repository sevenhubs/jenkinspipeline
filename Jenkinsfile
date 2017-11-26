pipeline {
    agent any /* utilizar todos los nodos disponibles */

	stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }
    }
}
