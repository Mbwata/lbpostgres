node {
    stage('validate') {
       sh '''liquibase tag $BUILD_NUMBER
            liquibase status --verbose'''
    }
    stage('update') {
       sh '''liquibase updateSQL
            liquibase update'''
    }
}
