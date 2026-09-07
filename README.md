# Pull Mysql Image
docker pull mysql

# Create docker network
docker network create two-tier -d bridge

# Create Image From Docker File 
docker build -t flask-app .

# Create Mysql Container From mysql Image
docker run -d --network two-tier --name mysql-db -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=task_db mysql


# Create Container from Image
docker run -d --network two-tier --name flask-container -p 5000:5000 -e DB_HOST=mysql-db -e DB_USER=root -e DB_PASSWORD=password -e DB_NAME=task_db flask-app
