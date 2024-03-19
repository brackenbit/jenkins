// Simple demo pipeline

// Define a pipeline
pipeline {
    // Specify an agent
    // i.e. what Jenkins node this should run on
    // Could have one Jenkins node set up with Maven, one with Gradle, etc.
    agent any

    // Define some stages
    stages {
        stage("Cleanup"){
            // Jenkins may leave remnants from previous builds in working folders.
            // Good practice to include a cleanup stage at the start of your pipeline.

            steps {
                // deleteDir() - recursively delete the current working directory from the workspace
                deleteDir()
            }
        }

        stage("Clone repo"){
            // (Not typically part of the process - the Jenkinsfile itself typically lives
            //  in SCM along with the source, so the repo would have been already
            //  downloaded, e.g. via SCM polling or schedule.)
            steps {
                // sh - run shell commands
                sh "git clone https://github.com/jenkins-docs/simple-java-maven-app.git"
            }
        }

        stage("Build"){
            steps {
                // dir - change directory
                // Any steps within the dir block will use this directory
                dir("simple-java-maven-app") {
                    sh "mvn clean install"
                    // clean - delete any existing compiled classes
                    // Shouldn't be required due to deleteDir() above, but a good practice.
                }
                
            }
        }

        stage("Test"){
            steps {
                dir("simple-java-maven-app") {
                    sh "mvn test"
                }
            }
        }
    }
}