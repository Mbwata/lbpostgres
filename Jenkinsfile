node {
    stage('validate') {
        //git branch '**': '', url: 'https://github.com/Mbwata/lbpostgres.git'
        checkout([$class: 'GitSCM', branches: [[name: '**']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Mbwata/lbpostgres.git']]])
        sh '''ls -l
            liquibase tag $BUILD_NUMBER
            liquibase status --verbose'''
    }
    stage('update') {
        sh '''liquibase updateSQL
            liquibase update'''
    }
}
