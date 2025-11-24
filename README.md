# 🚀 Spring Boot CI/CD Pipeline with Jenkins, SonarQube, Trivy, Docker & Amazon EKS

The entire pipeline is automated using **Jenkins**, including:
- Source code pull from GitHub  
- Code quality & security scan (SonarQube)  
- Docker image build  
- Trivy vulnerability scan  
- Push to DockerHub  
- Deployment to EKS

## 🏗️ **Architecture / Workflow**

https://github.com/bhupal2027/Spring_boot_APP_CI-CD/blob/09c74af8a0b88f00cf8e7d2ea5cd132c2e0dfa78/blueprint.jpg

1. **Developer pushes code to GitHub**
2. **Jenkins CI Pipeline triggers**
3. **Stages inside CI:**
   - Checkout code
   - Maven build (`mvn clean install`)
   - SonarQube scan
   - Docker image build
   - Trivy image scan
   - Push image to DockerHub
4. **CD Pipeline triggers after CI**
5. **Deploy the new image to Amazon EKS**
6. **Application becomes available via LoadBalancer/Ingress**

---

## 🧪 **Technologies Used**

| Tool | Purpose |
|------|---------|
| **Spring Boot** | Web application |
| **Maven** | Build and dependency management |
| **Jenkins** | CI/CD pipeline automation |
| **SonarQube** | Code quality analysis |
| **Trivy** | Docker image vulnerability scanning |
| **Docker** | Build + containerize application |
| **DockerHub** | Private image registry |
| **Amazon EKS** | Kubernetes cluster for deployment |
| **kubectl** | Deployment commands |
| **Helm (optional)** | Easy K8s deployment |

## 🐳 **Dockerfile**
FROM eclipse-temurin:11-jre

COPY target/*.jar app.jar

ENTRYPOINT ["java","-jar","/app.jar"]

🛠️ Jenkins CI/CD Pipeline (Jenkinsfile)

pipeline {

    agent none

    environment {
        GIT_URL         = 'https://github.com/bhupal2027/Spring_boot_APP_CI-CD'
        SONARQUBE_ID    = 'SonarQubeServer'
        IMAGE_NAME      = 'spring-boot-demo'
        DOCKERHUB_CREDS = 'dockerhub-creds'
        SONAR_TOKEN_ID  = 'mvn-sonar'
        AWS_CREDS_ID    = 'aws-creds'
        AWS_REGION      = 'ap-south-1'
        EKS_CLUSTER     = 'my-eks-cluster'
    }

    stages {

        stage('Checkout') {
            agent any
            steps {
                git branch: 'master', url: "${GIT_URL}"
            }
        }

        stage('SonarQube Scan') {
            agent {
                docker {
                    image 'maven:3.9.8-eclipse-temurin-17'
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                dir('spring-boot-app') {
                    withSonarQubeEnv("${SONARQUBE_ID}") {
                        withCredentials([string(credentialsId: SONAR_TOKEN_ID, variable: 'SONAR_TOKEN')]) {
                            sh """
                            mvn clean verify sonar:sonar \
                                -Dsonar.login=$SONAR_TOKEN \
                                -DskipTests \
                                -Dsonar.projectKey=${IMAGE_NAME}
                            """
                        }
                    }
                }
            }
        }

        stage('Quality Gate') {
            agent any
            steps {
                echo "Skipping Quality Gate because Jenkins cannot receive SonarQube webhook on local server."
            }
        }

        stage('Build JAR') {
            agent {
                docker {
                    image 'maven:3.9.8-eclipse-temurin-17'
                }
            }
            steps {
                dir('spring-boot-app') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Build Docker Image') {
            agent any
            steps {
                dir('spring-boot-app') {
                    sh """
                    docker build -t ${IMAGE_NAME}:latest .
                    """
                }
            }
        }

        stage('Trivy Scan') {
            agent any
            steps {
                sh """
                trivy image --exit-code 0 --severity HIGH,CRITICAL ${IMAGE_NAME}:latest
                """
            }
        }

        stage('Push to DockerHub') {
            agent any
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "${DOCKERHUB_CREDS}",
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh """
                    echo "$PASS" | docker login -u "$USER" --password-stdin
                    docker tag ${IMAGE_NAME}:latest $USER/${IMAGE_NAME}:latest
                    docker push $USER/${IMAGE_NAME}:latest
                    docker logout
                    """
                }
            }
        }

        stage('Deploy to EKS') {
            agent any
            steps {
                withAWS(credentials: "${AWS_CREDS_ID}", region: "${AWS_REGION}") {
                    sh """
                    echo 'Updating kubeconfig for EKS cluster...'
                    aws eks update-kubeconfig \
                        --region ${AWS_REGION} \
                        --name ${EKS_CLUSTER}

                    echo 'Applying Kubernetes Manifests...'
                    kubectl apply -f spring-boot-app/k8s/deployment.yaml
                    kubectl apply -f spring-boot-app/k8s/service.yaml

                    echo 'Deployment Successful!'
                    """
                }
            }
        }
    }
}

☸️ Kubernetes Deployment (k8s-deployment.yaml)

apiVersion: apps/v1
kind: Deployment
metadata:
  name: springboot-app
  labels:
    app: springboot-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: springboot-app
  template:
    metadata:
      labels:
        app: springboot-app
    spec:
      containers:
      - name: springboot-app
        image: bhupal716/spring-boot-demo:latest
        ports:
        - containerPort: 8080

***Service.yaml***
apiVersion: v1
kind: Service
metadata:
  name: springboot-service
spec:
  type: LoadBalancer
  selector:
    app: springboot-app
  ports:
    - port: 80
      targetPort: 8080

**🌐 Access the Application**
After deployment, run:
kubectl get svc
You will get an external LoadBalancer URL or else you can check in Loadbalancer Section.

I got below output.

https://github.com/bhupal2027/Spring_boot_APP_CI-CD/blob/af68ea57ebd8f5aea2586b616c90646a615e21cf/output%20from%20Load%20balancer.png
