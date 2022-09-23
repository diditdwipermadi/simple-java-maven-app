node {
    stage('Build') {
        withMaven(maven: 'mvn') {
            sh 'mvn -B -DskipTests clean package'
        }
    }
    stage('Test') {
        withMaven(maven: 'mvn') {
            sh 'mvn test'
        }
            junit 'target/surefire-reports/*.xml'
    }
    stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?? (Klik "Proceed" untuk melanjutkan eksekusi pipeline ke tahap Deploy)'
    }
    stage('Deploy') {
        withMaven(maven: 'mvn') {
            sh './jenkins/scripts/deliver.sh'
        }
            echo 'Waiting 1 minutes for deployment to complete'
            sleep 60     // seconds
    }
}