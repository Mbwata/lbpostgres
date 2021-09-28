node {
    stage('validate') {
        git branch: '', url: 'https://github.com/Mbwata/lbpostgres.git'
        sh '''ls -l
            liquibase tag $BUILD_NUMBER
            liquibase status --verbose'''
    }
    stage('update') {
        sh '''liquibase updateSQL
            liquibase update'''
    }
}
