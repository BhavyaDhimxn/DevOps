🚀 FastAPI App with Docker and GitHub Actions CI/CD

This project is a FastAPI application containerized using Docker, with GitHub Actions for Continuous Integration and Continuous Deployment (CI/CD).

🔥 1. Installation and Running Locally

✅ Prerequisites
Python (>=3.8)
pip and venv
Docker (for containerization)
🔧 Local Setup Instructions
Clone the Repository:
git clone https://github.com/BhavyaDhimxn/DevOps.git
cd DevOps
Create and Activate Virtual Environment:
python3 -m venv venv
source venv/bin/activate  # On Linux/Mac
venv\Scripts\activate     # On Windows
Install Dependencies:
pip install --upgrade pip
pip install -r requirements.txt
Run the FastAPI Server:
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
Access the API:
Open your browser and visit: http://localhost:8000
Interactive API docs: http://localhost:8000/docs
🐳 2. Build and Run Docker Image

✅ Prerequisites
Docker installed and running.
🔧 Steps to Build and Run with Docker
Build the Docker Image:
docker build -t fastapi-app .
Run the Docker Container:
docker run -p 8000:8000 fastapi-app
Verify the API:
Open your browser: http://localhost:8000
Interactive Swagger docs: http://localhost:8000/docs
🔥 Push Docker Image to Docker Hub
Login to Docker Hub:
docker login -u <your-docker-username> -p <your-docker-token>
Tag the Image:
docker tag fastapi-app <your-docker-username>/fastapi-app:latest
Push to Docker Hub:
docker push <your-docker-username>/fastapi-app:latest
⚙️ 3. GitHub Actions Workflow Explanation

This project uses GitHub Actions to automate building and pushing Docker images.

✅ Workflow Trigger
The workflow is triggered on every push event to the main branch.
✅ Workflow Steps
Checkout Repository:
Pulls the latest code from GitHub.
- name: Checkout Repository
  uses: actions/checkout@v4
Set up Docker Buildx:
Allows building multi-platform images.
- name: Set up Docker Buildx
  uses: docker/setup-buildx-action@v2
Docker Login:
Authenticates with Docker Hub using GitHub Secrets.
- name: Docker Login
  uses: docker/login-action@v2
  with:
    username: ${{ secrets.DOCKER_USERNAME }}
    password: ${{ secrets.DOCKER_PASSWORD }}
Build and Push Docker Image:
Builds a multi-platform image (amd64 and arm64) and pushes it to Docker Hub.
- name: Build and Push Docker Image
  run: |
    docker buildx build \
      --platform linux/amd64,linux/arm64 \
      -t <your-docker-username>/fastapi-app:latest . \
      --push
🔥 4. Setting up Docker Token and GitHub Secrets

✅ Step 1: Generate Docker Hub Token
Go to Docker Hub and log in.
Navigate to Account Settings → Security.
Click New Access Token → Name it (e.g., github-actions) → Select read/write.
Copy the generated token.
✅ Step 2: Add GitHub Secrets
Go to your GitHub repository → Settings → Secrets and Variables → Actions.
Click on New Repository Secret.
Add the following secrets:
DOCKER_USERNAME: Your Docker Hub username.
DOCKER_PASSWORD: Your Docker Hub Access Token.
Save the secrets.
✅ Step 3: Test GitHub Actions
Push your code to the main branch.
Go to GitHub → Actions and verify the workflow execution.
After a successful build, you will find the Docker image in your Docker Hub account.
📚 5. API Endpoints

GET /
Returns a welcome message.
GET /items/{item_id}
Fetches an item by ID.
POST /items/
Creates a new item.
Request Body Example:
{
  "name": "Tiger",
  "description": "Big Cat",
  "price": 1500,
  "tax": 0.15
}
🚀 6. Project Structure

/app
 ├── Dockerfile               # Docker instructions for building the image
 ├── requirements.txt         # Python dependencies
 ├── main.py                  # FastAPI application
 ├── .github/workflows        # GitHub Actions CI/CD workflow
 ├── .dockerignore            # Files to ignore when building Docker image
 ├── README.md                # Project documentation
🎯 7. Key Commands Cheat Sheet

✅ Run Locally

uvicorn main:app --reload
✅ Build Docker Image

docker build -t fastapi-app .
✅ Run Docker Container

docker run -p 8000:8000 fastapi-app
✅ Push Docker Image to Docker Hub

docker tag fastapi-app <your-docker-username>/fastapi-app:latest
docker push <your-docker-username>/fastapi-app:latest
🚀 8. Contributing

Fork the repo.
Create a feature branch (git checkout -b feature-branch).
Commit your changes (git commit -m 'Add new feature').
Push to the branch (git push origin feature-branch).
Create a pull request.
