pipeline {
    agent any // utilizar todos los nodos disponibles

	stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                // ejecutar "job" existente en Jenkins
                build job: 'deploy-to-staging'
            }
        }

        stage ('Deploy to Production'){
            steps {
                timeout(time: 5, unit: 'DAYS') {                    // después de 5 días sin aprobación el "job" falla
                    input message: 'Approve PRODUCTION Deployment?' // muestra el mensaje en Jenkins y requiere que
                                                                    // el usuario acepte
                }

                build job: 'deploy-to-prod'
            }
            post {
                success {
                    echo 'Code deployed to Production.'
                }

                failure {
                    echo 'Deployment failed.'
                }
            }
        }
    }
}
