pipeline {
  agent {
    node {
      label 'min-centos-7-x64'
    }
    
  }
  stages {
    stage('Prepare') {
      steps {
        sh '''                    sudo yum -y install centos-release-scl-rh
                    sudo yum -y install rh-git29
                    sudo yum -y remove git
                    sudo ln -fs /opt/rh/rh-git29/root/usr/bin/git /usr/bin/git
                    sudo ln -fs /opt/rh/httpd24/root/usr/lib64/libcurl-httpd24.so.4 /usr/lib64/libcurl-httpd24.so.4
                    sudo ln -fs /opt/rh/httpd24/root/usr/lib64/libnghttp2-httpd24.so.14 /usr/lib64/libnghttp2-httpd24.so.14'''
      }
    }
    stage('Build client source') {
      steps {
        sh 'sg docker -c "./build/bin/build-pmm-client-source-tarball"'
      }
    }
    stage('Build client binary') {
      steps {
        sh 'sg docker -c "./build/bin/build-pmm-client-binary-tarball"'
      }
    }
  }
}