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
                rtMavenDeployer (
                    id: "GOL_DEPLOYER",
                    serverId: "JFROG_CLOUD",
                    releaseRepo: 'uv-libs-snapshot-local',
                    snapshotRepo: 'uv-libs-snapshot-local'
                )
                rtMavenRun (
                    tool: 'MAVEN_3.9', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "GOL_DEPLOYER",
                    buildName: "${JOB_NAME}",
                    buildNumber: "${BUILD_ID}"
                )
                rtPublishBuildInfo (
                    serverId: "JFROG_CLOUD"
                )
            }
        }
        // stage('SonarQube analysis') {
        //     steps {
        //         // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
        //         withSonarQubeEnv('SONAR_CLOUD') {
        //         // requires SonarQube Scanner for Maven 3.2+
        //             sh 'mvn clean package sonar:sonar -Dsonar.organization=urvashiharode -Dsonar.token=0dabf4de36f624a79198845b6dd00b78bfa56465 -Dsonar.projectKey=gameoflife'
        //         }
        //     }
        // }
        stage('junit') {
            steps {
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}