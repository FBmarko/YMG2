pipeline{
    agent any
    triggers{
        githubPush()
    }
    environment{
        PATH = "C:\\Program Files\\Docker\\Docker\\resources\\bin;$PATH"
        IMAGE_NAME="ymg-img"
        CONTAINER_NAME="nginx-container"
    }
    stages{
        stage('Repo Klonla'){
            steps{
                git url: 'https://github.com/FBmarko/YMG2.git', branch: 'main'
            }
        }
        stage('Docker Image Olustur'){
            steps{
                echo "Docker Image Oluşturuldu"
            bat "docker build -t ${IMAGE_NAME} ."
            }
        }
        stage('Eski conteyniri Durdur'){
            steps{
                echo "Eski conteyner durduruldu"
                bat "docker rm -f ${CONTAINER_NAME}|| true " 
            }
        }
        stage('Yeni conteyniri Olustur'){
            steps{
                echo "Yeni Conteyner Oluştu"
                bat "docker run -d --name ${CONTAINER_NAME} -p 5050:80 ${IMAGE_NAME}"
            }
        }
        }
    post{
        success{
            echo "Yayin basarili:http://localhost:5050"
        }
        failure{
            echo "Pipeline basarisiz oldu"
        }
    }    
}
