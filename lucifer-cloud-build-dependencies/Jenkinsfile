pipeline {
    agent any

    environment{
            gitUrl = "http://192.168.137.200/lucifer-cloud/lucifer-cloud-build.git"
            gitCredentialsId = "b77c3db3-1b8b-4719-804c-f344e51e2ad7"
            mvn_home = "/data/maven/maven-3.9.4/"
     }

    // hidden 标签jenkins需要安装 Hidden Parameter 插件
    parameters {
          choice choices: ['*/master', '*/dev'], description: '选择的branch', name: 'branch'
       }


    // 存放所有任务的合集
    stages {
        // 拉取Git代码
        stage('checkout code from gitlab...') {
            steps {
                checkout scmGit(branches: [[name: "${branch}"]], extensions: [], userRemoteConfigs: [[credentialsId: "${gitCredentialsId}", url: "${gitUrl}"]])
            }
        }

        // 检测代码质量
        stage('code quality...') {
            steps {
                echo '检测代码质量'
            }
        }

        // 构建代码
        stage('mvn build code...') {
            steps {
                sh '${mvn_home}/bin/mvn clean package -DskipTests'
            }
        }
    }
}
