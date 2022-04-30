node {
    stage('SCM Checkout'){
        git branch: 'feature', url: 'https://github.com/sandeepmchary/java_home.git'
    }
    stage('Mvn Package'){
        sh "mvn clean package"
    }
}
