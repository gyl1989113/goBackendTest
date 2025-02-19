pipeline {
    agent none  // No global agent; specify per stage
    triggers {
        githubPush()
    }
    stages {
        stage('Checkout') {
            agent { label 'master' }  // Specify the agent for this stage
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '**']],  // Match any branch or tag
                          userRemoteConfigs: [[
                            url: 'https://github.com/gyl1989113/goBackendTest.git',
                            credentialsId: 'github-auth'
                        ]]])
            }
        }

        stage('编译打包') {
            agent { label 'master' }  // Specify the agent for this stage
            steps {
                script {
                    def imageTag = env.BRANCH_NAME.replaceAll('/', '-')
                    sh """
                        ls -al
                        docker build -t backend:${imageTag} .
                    """
                }
            }
        }
    }
}
