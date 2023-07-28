pipeline {
    agent none

    tools {
        // Install the Maven version configured as "mymaven" and JDK version configured as "myjava" and add them to the path.
        maven "mymaven"
        jdk "myjava"
    }

    stages {
        stage('Compile') {
            agent any
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/edureka-git/DevOpsClassCodes.git'

                // Run Maven on a Unix agent.
                sh "mvn compile"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }

        stage('CodeReview') {
            agent any
            steps {
                sh "mvn pmd:pmd"
            }
        }

        stage('UnitTest') {
            agent any
            steps {
                sh "mvn test"
            }
        }

        stage('MetricCheck') {
            agent any
            steps {
                sh "mvn cobertura:cobertura -Dcobertura.report.format=xml"
            }
        }

        stage('Package') {
            agent any
           
            steps {
                sh "mvn package"
            }
        }
    }
}
