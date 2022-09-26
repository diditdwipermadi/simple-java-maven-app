node {
    
    env.AWS_ACCESS_KEY_ID     = credentials('jenkins-aws-secret-key-id')
    env.AWS_SECRET_ACCESS_KEY = credentials('jenkins-aws-secret-access-key')
      
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
            sh 'java -jar target/my-app-1.0-SNAPSHOT.jar'
            echo 'Waiting 1 minutes for deployment to complete'
            sleep 60
    }
}