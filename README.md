# .github/workflows/docker-build.yml
name: 🐳 Docker Build & Push

on:
  push:
    branches: [main]

jobs:
  docker:
    name: 🔧 Build & Push Docker Imag
    runs-on: ubuntu-latest

    steps:
    - name: 📥 Checkout code
      uses: actions/checkout@v3

    - name: 🔐 Log in to Docker Hub
      uses: docker/login-action@v2
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}

    - name: 🏗 Build Docker image
      run: |
        docker build -t ${{ secrets.DOCKER_USERNAME }}/my-app:latest .

    - name: 🚀 Push image to Docker Hub
      run: |
        docker push ${{ secrets.DOCKER_USERNAME }}/my-app:latest
