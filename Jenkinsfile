// pipeline {
// agent any
// stages {

//     stage('Build Docker Image') {
//         steps {
//             sh 'docker build -t nodeapp:${BUILD_NUMBER} .'
//         }
//     }
// }
// }
pipeline {
agent any
environment {
    IMAGE_NAME = "nodeapp"
    CONTAINER_NAME = "nodeapp-container"
}
stages {

    stage('Build Docker Image') {
        steps {
            sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .'
        }
    }
    stage('Stop Old Container') {
        steps {
            sh '''
            docker stop ${CONTAINER_NAME} || true
            docker rm ${CONTAINER_NAME} || true
            '''
        }
    }

    stage('Run New Container') {
        steps {
            sh '''
            docker run -d \
            --name ${CONTAINER_NAME} \
            -p 3000:3000 \
            ${IMAGE_NAME}:${BUILD_NUMBER}
            '''
        }
    }
}

}

