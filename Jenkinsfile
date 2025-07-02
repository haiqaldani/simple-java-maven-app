node {
    try {
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }
        
        stage('Test') {
            sh 'mvn test'
            
            step([$class: 'JUnitResultArchiver', testResults: 'target/surefire-reports/*.xml'])
        }

        stage('Deliver') {
            sh '/jenkins/scripts/deliver.sh'
        }
    } catch (err) {
        currentBuild.result = 'FAILURE'
        throw err
    }
}
