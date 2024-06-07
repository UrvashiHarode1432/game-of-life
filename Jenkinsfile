pipeline {
    agent { label 'JDK-8' }
    tools { jdk 'JDK_8' }
    stages {
        stage('vsc') {
            step {
                git branch: 'master', url: 'https://github.com/UrvashiHarode1432/game-of-life.git'
            }
        }
        stage('build') {
            step {
                sh script: 'mvn package'
            }
        }
        stage('artifacts') {
            step {
                archiveArtifacts artifacts: '**/gameoflife.war'
            }
        }
        stage('junit') {
            step {
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}