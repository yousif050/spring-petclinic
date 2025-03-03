pipeline {
    agent any
    triggers {
      //Every 3min monday
        cron('H/3 * * * 1')
    }
    stages {
        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }
        stage('Test & JaCoCo Report') {
            steps {
              //Test
                sh './mvnw test jacoco:report'
            }
            post {
                always {
                    // publish the JaCoCo report 
                    jacoco(
                        execPattern: '**/target/jacoco.exec',
                        classPattern: '**/target/classes',
                        sourcePattern: '**/src/main/java',
                        exclusionPattern: '**/src/test/**'
                    )
                }
            }
        }
    }
}
