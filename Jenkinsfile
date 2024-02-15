pipeline{
    agent {label 'JDK17'}
    options {
        timeout(time: 30, unit: 'MINUTES') 
    }
    triggers { pollSCM('* * * * *') }
    tools {
        jdk 'JDK_8' 
    }
    stages{
        stage('vcs'){
            steps{
                git url: 'https://github.com/ssardhana/game-of-life.git',
                    branch: 'develop'
            }

        }
        stage('build and package'){
            steps{
                sh script: 'mvn package'        
            }
        }
        stage('reporting'){
            steps{
                //archiveArtifacts artifacts: '**/targets/gameoflife.war'
                junit testResults: '/gol-declarative/gameoflife-web/target/surefire-reports/TEST-behavior.CountingThings.xml'
            }
        }
    }
}