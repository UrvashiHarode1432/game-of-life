pipeline {
    agent { label 'JDK-8' }
    tools { jdk 'JDK_8' }
    stages {
        stage('vsc') {
            steps {
                git branch: 'master', url: 'https://github.com/UrvashiHarode1432/game-of-life.git'
            }
        }
        stage('build') {
            steps {
                sh script: 'mvn package'
            }
        }
        stage('artifacts') {
            steps {
                archiveArtifacts artifacts: '**/gameoflife.war'
            }
        }
        stage('junit') {
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}