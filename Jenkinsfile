@Library('shared-lib') _
import org.example.MyUtils

pipeline {
    agent any
    stages {
        stage('Greet') {
            steps {
                sayHello('Jeremy')
            }
        }
        stage('Shout') {
            steps {
                script {
                    def message = MyUtils.shout('jenkins at scale')
                    echo message
                }
            }
        }
    }
}
