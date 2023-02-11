pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'first jenkins pipeline'
        sh '''./mvnw clean compile
'''
      }
    }

    stage('Unit Test') {
      steps {
        sh '''./mvnw test
'''
        junit '**/target/surefire-reports/TEST-*.xml'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.projectKey=JPetstore \\
  -Dsonar.host.url=http://44.205.255.188:9000 \\
  -Dsonar.login=sqp_3a3ebdb1f58893374bf9e6d36613759b0f9e0b9d'''
      }
    }

    stage('Package') {
      steps {
        sh '''./mvnw package -DskipTests=true
'''
      }
    }

    stage('Deploy') {
      steps {
        node(label: 'test') {
          sh '''./mvnw spring-boot:run </dev/null &>/dev/null &
'''
        }

      }
    }

  }
}