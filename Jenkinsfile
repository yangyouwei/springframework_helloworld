pipeline {

    agent any

    options {
        disableConcurrentBuilds()
        timeout(time: 1, unit: 'HOURS')
        timestamps ()
   }


    environment {
        LOCAL_SOURCE_DIR = "/var/jenkins_home/workspace/test-demo"
        DOCKER_DIR = "/var/jenkins_home/workspace/test-demo/docker"
        LOCAL_BUILD_WORKDIR = "/var/jenkins_home/workspace/test-demo/test-project/src"
        JAR_PACKAGE_NAME = "demo-0.0.1-SNAPSHOT.jar"
        IMAGE = "192.168.28.133/tccp/demo:v0.1"
   }
    
    stages {

        stage ("下载代码") {
            steps {
                echo "下载代码"
                sh "git clone git@gitee.com:gudaoyufu/test-project.git"
            }
        }

        stage ("构建打包") {
            steps {
                echo "构建打包"
                sh "cd ${LOCAL_BUILD_WORKDIR}"
                withMaven(maven: 'M3') {
							// Run the maven build
							sh "mvn clean package"
						}
            }
        }

        stage ("docker打包成镜像"){
            steps {
                echo "docker打包成镜像"
                sh "cd ${DOCKER_DIR}"
                sh "cp ${LOCAL_SOURCE_DIR}/target/${JAR_PACKAGE_NAME} ${DOCKER_DIR}"
                sh "cd ${DOCKER_DIR} && docker build -t ${IMAGE} ."
                sh "docker-compose up -d"
            }
        }

       

        }
    }