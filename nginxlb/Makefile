status:
	sudo docker ps -a
all:
	sudo docker build -t mylb .
	sudo docker images
run:
	sudo docker run -p 80:80 -p 8080:8080 -p 50000:50000 -p 8000:8000 --name mylb -d mylb