pipeline {
    agent any

    environment{
            harborUser = 'DevOps'
            harborPasswd = 'lucifer1@DevOps'
            gitUrl = "http://192.168.137.200/lucifer-cloud/lucifer-cloud-build.git"
            gitCredentialsId = "b77c3db3-1b8b-4719-804c-f344e51e2ad7"
            mvn_home = "/data/maven/maven-3.9.4/"
            publisher_host = "192.168.137.133"
            publisher_hostName = "k8s-master-1"
            deployment = "hello-lucifer"
            namespace = "kube-lucifer" ;
     }

    // hidden 标签jenkins需要安装 Hidden Parameter 插件
    parameters {
          choice choices: ['*/master', '*/dev'], description: '选择的branch', name: 'branch'
          string name: 'tag', defaultValue: '1.1.1', description:'镜像标签', trim: true
          hidden name: 'harborHost', defaultValue: '192.168.137.199:80', description:'镜像私服地址'
          hidden name: 'harborRepo', defaultValue: 'lucifer_repository', description:'镜像仓库'
          hidden name: 'publisher_remoteDirectory', defaultValue: '/data/deploy/hello-lucifer/', description:'ssh远程文件夹'
          hidden name: 'publisher_sourceFiles', defaultValue: 'deploy.yaml', description:'ssh远程构建文件'
          hidden name: 'publisher_sourceFiles_env', defaultValue: 'deploy-env.yaml', description:'ssh远程临时环境变量文件'
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
