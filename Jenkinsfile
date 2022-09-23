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
    stage('Deploy') {            
            sh './jenkins/scripts/deliver.sh'
            input message: 'Sudah selesai menggunakan Java App? (Klik "Proceed" untuk mengakhiri)'
            sh './jenkins/scripts/kill.sh'
        }
}