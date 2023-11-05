pipeline {
    agent any
    stages {
        stage("SCM_Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/ManaasGupta/course3-jenkins-gs-spring-petclinic.git'
            }
        }
        stage("Compiling_Project") {
            steps {
                sh "./mvnw compile"
            }
        }
        stage("Testing") {
            steps {
                sh "./mvnw test"
            }
        }
        stage("Packaging_Project") {
            steps {
                sh "./mvnw package"
            }
        }
        stage("Archiving_Package") {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            }
        }
        stage("Junit_Results") {
            steps {
                junit '**/target/surefire-reports/TEST*.xml'
            }
        }

        stage("Archiving_Jacoco_Report") {
            steps {
                jacoco()
            }
        }
    }
    post {
        always {
            emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}",
                subject: "${currentBuild.currentResult}: ${currentBuild.fullDisplayName} [${env.BUILD_NUMBER}]",
                to: "manas@foo.bar"
        }
    }
}