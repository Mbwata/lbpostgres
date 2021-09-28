stage('validate') {
    liquibase tag $BUILD_NUMBER
    liquibase status --verbose

}



pipeline {
    agent any

    stages {
        
        stage('validate') {
            liquibase tag $BUILD_NUMBER
            liquibase status --verbose

        }       
    }
}