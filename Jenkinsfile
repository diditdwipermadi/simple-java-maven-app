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
        
        sshagent (credentials: ['ssh-ec2-user']) {
          sh "scp target/my-app-1.0-SNAPSHOT.jar ec2-user@ec2-52-77-222-40.ap-southeast-1.compute.amazonaws.com:/var/www/html/dicoding"
        }
            echo 'Waiting 1 minutes for deployment to complete'
            sleep 60
    }
}