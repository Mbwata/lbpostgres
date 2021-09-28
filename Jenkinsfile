stage('validate') {
    liquibase tag $BUILD_NUMBER
    liquibase status --verbose

}