# springboot-k8s-mysql
Download project from github https://github.com/dpise/springboot-k8s-mysql.git

1. First do maven build to create jar/war file in target folder

2. First create docker image by command

docker build image -t dpise17/springbootmysqldemo .

3. Then tag the image 

docker tag dpise17/springbootmysqldemo:latest dpise17/springbootmysqldemo:v1

4. then push the image in docker repository

	4.1 do docker login
	4.2 docker push dpise17/springbootmysqldemo:v1

5. Start minikube cluster

	c:> minikube start
	
6. go to path in project directory where can see .ymal file.

		e.g. F:\AzureKalyan\Spring Boot docker+MySQL+Kube\springboot-k8s-mysql\src\main\resources>
		
7. then run create namespace
	kubectl create namespace springmysql
	
8. Then run below files in given sequence

		kubectl apply -f <filename> -n springmysql
		
		-mysql-configmap.yml
		-mysqldb-root-credentials.yml
		- mysqldb-credentials.yml
		- mysql-deployment.yml
		- deployment.yml
		
		Note -  if need to remove then apply kubectl delete -f <filename> -n namespace
		
9. In minikube there is no public ip so no loadbalancer type.

10. get the service name of deployment 

	c:> minikube get service -n namespace
	
	11. Run the service
	
	minikube service <service name of deployment> -n springmysql
	
	e.g. minikube service springboot-k8s-mysql -n springmysql
	
	it will show the ip address. run the command http://192.168.99.104:30163/users
	
