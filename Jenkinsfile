pipeline {

    agent any

    options {
        disableConcurrentBuilds()
        timeout(time: 1, unit: 'HOURS')
        timestamps ()
   }


    environment {
        LOCAL_SOURCE_DIR = "/var/jenkins_home/workspace/javatest"
        LOCAL_BUILD_WORKDIR = "/var/jenkins_home/workspace/javatest/springframework_helloworld/src"
   }
    
    stages {

        stage ("下载代码") {
            steps {
                echo "下载代码"
                sh "git clone https://github.com/yangyouwei/springframework_helloworld.git"
            }
        }

        stage ("构建打包") {
            steps {
                echo "构建打包"
                sh "cd ${LOCAL_BUILD_WORKDIR}"
                sh "pwd"
                withMaven(maven: 'M3') {
							// Run the maven build
							sh "mvn clean package"
						}
            }
        }
    }
}
