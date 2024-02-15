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
                archiveArtifacts artifacts: '**/target/*.war'
                junit testResults: '**/target/surefire-reports/TEST-*.xml'
            }
        }
    }
}