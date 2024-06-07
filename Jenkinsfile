pipeline {
    agent { label 'JDK-8' }
    tools { jdk 'JDK_8' }
    parameters {
        choice(name: 'GOAL', 
        choices: ['package', 'clean package', 'install', 'clean install'])
    }
    stages {
        stage('vsc') {
            steps {
                git branch: 'master', url: 'https://github.com/UrvashiHarode1432/game-of-life.git'
            }
        }
        stage('build') {
            steps {
                sh script: "mvn ${params.GOAL}"
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