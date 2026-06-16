🩺 Medical RAG Chatbot - Complete CI/CD Documentation
🚀 Jenkins + Docker + Trivy + AWS ECR + AWS App Runner
✨ Project Overview
This project builds a Medical RAG Chatbot and deploys it through a modern CI/CD pipeline. The workflow includes Dockerization, Jenkins automation, vulnerability scanning with Trivy, image publishing to AWS ECR, and deployment to AWS App Runner.
🛠️ Technology Stack
•	🐍 Python + RAG application
•	🐳 Docker Desktop and Jenkins Docker image
•	🔧 Jenkins CI/CD
•	🛡️ Trivy vulnerability scanner
•	☁️ AWS ECR and AWS App Runner
•	🔐 GitHub token-based integration
🔧 Corrections Applied
•	Cleaned up wording and formatting for a professional README/doc style.
•	Corrected Docker command formatting and Windows line-break style.
•	Added better structure for Jenkins, Trivy, ECR, and App Runner steps.
•	Marked manual steps clearly where AWS console actions are required.
•	Standardized stage flow from source to deployment.
1️⃣ Clone and Local Setup
•	Clone the project repository from GitHub.
git clone https://github.com/data-guru0/LLMOPS-2-TESTING-MEDICAL.git
cd LLMOPS-2-TESTING-MEDICAL
•	Create a virtual environment on Windows.
python -m venv venv
venv\Scripts\activate
•	Install project dependencies.
pip install -e .
•	Prerequisites checklist before moving forward: Docker Desktop is installed and running in the background, code versioning is set up using GitHub, Dockerfile is created for the project, and Dockerfile is also created for Jenkins.
2️⃣ Jenkins Setup for Deployment
•	Create a folder named custom_jenkins and add a Dockerfile inside it with Jenkins + Docker-in-Docker configuration.
•	Build the Jenkins Docker image.
cd custom_jenkins
docker build -t jenkins-dind .
•	Run the Jenkins container using Docker Desktop.
docker run -d ^
  --name jenkins-dind ^
  --privileged ^
  -p 8080:8080 ^
  -p 50000:50000 ^
  -v /var/run/docker.sock:/var/run/docker.sock ^
  -v jenkins_home:/var/jenkins_home ^
  jenkins-dind
•	Check Jenkins logs and get the initial password.
docker ps
docker logs jenkins-dind
•	If the password is not visible, read it directly from the container.
docker exec jenkins-dind cat /var/jenkins_home/secrets/initialAdminPassword
•	Open Jenkins dashboard at http://localhost:8080.
•	Install Python inside the Jenkins container.
docker exec -u root -it jenkins-dind bash
apt update -y
apt install -y python3
python3 --version
ln -s /usr/bin/python3 /usr/bin/python
python --version
apt install -y python3-pip
exit
•	Restart Jenkins container after installation.
docker restart jenkins-dind
•	Sign in again to Jenkins dashboard.
3️⃣ Jenkins Integration with GitHub
•	Generate a GitHub personal access token from GitHub settings.
•	Use scopes: repo and admin:repo_hook.
•	Add the GitHub token to Jenkins credentials as github-token.
•	Create a new Jenkins pipeline job, for example medical-rag-pipeline.
•	Use Pipeline Syntax to generate the checkout script for your GitHub repository.
•	Create a Jenkinsfile in the project root if not already present.
•	Push the Jenkinsfile to GitHub.
git add Jenkinsfile
git commit -m "Add Jenkinsfile for CI pipeline"
git push origin main
•	Run the pipeline from Jenkins and confirm checkout works successfully.
4️⃣ Build, Scan, and Push to AWS ECR
•	Install Trivy inside the Jenkins container.
docker exec -u root -it jenkins-dind bash
apt install -y
curl -LO https://github.com/aquasecurity/trivy/releases/download/v0.62.1/trivy_0.62.1_Linux-64bit.deb
dpkg -i trivy_0.62.1_Linux-64bit.deb
trivy --version
exit
•	Restart Jenkins container after installing Trivy.
docker restart jenkins-dind
•	Install AWS plugins in Jenkins: AWS SDK and AWS Credentials.
•	Create an IAM user in AWS with programmatic access and attach AmazonEC2ContainerRegistryFullAccess.
•	Add AWS credentials to Jenkins as aws-ecr-creds.
•	Install AWS CLI inside the Jenkins container.
docker exec -u root -it jenkins-dind bash
apt update
apt install -y unzip curl
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
./aws/install
aws --version
exit
•	Create an ECR repository in AWS and note the repository URI.
•	Add build, scan, and push stages in your Jenkinsfile if not already present.
•	Tip: Use Trivy with --exit-code 0 for reporting, or --exit-code 1 to fail the pipeline on vulnerabilities.
•	If Docker socket permission issues appear, fix them inside the Jenkins container.
docker exec -u root -it jenkins-dind bash
chown root:docker /var/run/docker.sock
chmod 660 /var/run/docker.sock
getent group docker
usermod -aG docker jenkins
exit
docker restart jenkins-dind
5️⃣ Deployment to AWS App Runner
•	Attach AWSAppRunnerFullAccess to the Jenkins IAM user if needed.
•	Go to AWS App Runner and create a new service.
•	Choose source as Container registry (ECR) and select your pushed image.
•	Configure CPU, memory, and environment variables as required.
•	Enable auto-deploy from ECR if you want automatic updates.
•	Deploy the service and verify that the app is live.
•	Run the Jenkins pipeline again to confirm the full flow works from checkout to deployment.
🏁 Final CI/CD Flow
GitHub → Jenkins → Build Docker Image → Trivy Scan → Push to ECR → Deploy to App Runner
This creates a complete automated deployment pipeline for your Medical RAG Chatbot.
