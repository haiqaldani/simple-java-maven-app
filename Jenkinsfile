node {
    try {
        stage('Build and Test') {
            docker.image('maven').inside {
                sh 'mvn -B -DskipTests clean package'
                sh 'mvn test'
                step([$class: 'JUnitResultArchiver', testResults: 'target/surefire-reports/*.xml'])
            }
        }

        stage('Deliver') {
            docker.image('maven').inside {
                sh './jenkins/scripts/deliver.sh'
            }
        }

    } catch (err) {
        currentBuild.result = 'FAILURE'
        throw err
    }
}
