all:
	docker info
	kubectl version

docker_deploy:
	docker run -d --name c5db --restart=always -p 50006:3306 \
	-e MYSQL_ROOT_PASSWORD=1234Qwer -e MYSQL_USER=c5dbadmin \
	-e MYSQL_PASSWORD=1234Qwer -e MYSQL_DATABASE=c5db kube-master:5000/mariadb

	docker run -d --name c5web --restart=always --link c5db \
	-p 50080:80 -p 50443:443 kube-master:5000/concrete5.7

docker_clean:
	docker kill c5db c5web
	docker rm c5db c5web

kube_status:
	kubectl get rc,svc,pods,pv,pvc

kube_deploy:
	kubectl create -f 1-mariadb-pod.yaml
	kubectl create -f 2-mariadb-svc.yaml
	kubectl create -f 3-concrete5-vol.yaml
	kubectl create -f 4-concrete5-rc.yaml
	kubectl create -f 5-concrete5-svc.yaml

kube_clean:
	kubectl delete svc concrete5
	kubectl delete rc  concrete5
	kubectl delete pvc pvcacmeapache
	kubectl delete pv  pv5gacmeapache
	kubectl delete pvc pvcacmehtml
	kubectl delete pv  pv5gacmehtml
	kubectl delete svc mariadb
	kubectl delete pod mariadb

kube_test: kube_status
	@echo "Assuming it is working"