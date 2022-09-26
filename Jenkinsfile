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
            sh 'mvn jar:jar install:install help:evaluate -Dexpression=project.name'
        }
            //sh 'java -jar target/my-app-1.0-SNAPSHOT.jar'
        withAWS(credentials: 'aws-credentials', region: 'ap-southeast-1') {
            sh 'aws s3 cp ./target/my-app-1.0-SNAPSHOT.jar s3://my-jars-1105/my-app-1.0.jar'
        }
            echo 'Waiting 1 minutes for deployment to complete'
            sleep 60
    }
}