node {
    stage('validate') {
       sh '''ls -l
            liquibase tag $BUILD_NUMBER
            liquibase status --verbose'''
    }
    stage('update') {
       sh '''liquibase updateSQL
            liquibase update'''
    }
}
