pipeline {
    agent none
    stages {
        stage('A') {
            steps {
                echo '执行A'
            }
            post {
                always {
                    echo '阶段A完成-always'
                }
                success {
                    echo '阶段A-成功'
                }
                failure {
                    echo '阶段A-失败'
                }
            }
        }
        stage('B') {
            input {
                message 'Should we continue?'
                ok 'Yes, we should.'
                submitter 'alice,bob'
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo '这个是一个带input的'
            }
            post {
                always {
                    echo '阶段A完成-always'
                }
                success {
                    echo '阶段A-成功'
                }
                failure {
                    echo '阶段A-失败'
                }
            }
        }
        stage('http请求') {
            steps {
                script {
                    def response = httpRequest 'https://www.baidu.com/'
                    println(response)
                }
            }
        }
        stage('并行节点') {
            when {
                //判断流水线是否执行这个阶段
                branch 'main'
            }
            failFast true//其中一个stage失败所有的终止
            parallel {
                stage('Branch A') {
                    input {
                        message 'Should we continue?'
                        ok 'Yes, we should.'
                        submitter 'alice,bob'
                        parameters {
                            string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                        }
                    }
                    steps {
                        echo 'On Branch A'
                    }
                }
                stage('Branch B') {
                    input {
                        message 'Should we continue?'
                        ok 'Yes, we should.'
                        submitter 'alice,bob'
                        parameters {
                            string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                        }
                    }
                    steps {
                        echo 'On Branch B'
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'always'
        }
        success {
            echo 'success'
        }
        failure {
            echo 'failure'
        }
    }
}
