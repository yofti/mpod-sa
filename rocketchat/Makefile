status:
	kubectl get rc,svc,pods -o wide

clean:
	kubectl delete pod mongo
	kubectl delete svc mongo
	kubectl delete rc rocketchat
	kubectl delete svc rocketchat
 
all:
	kubectl create -f 1-mongo-pod.yaml
	kubectl create -f 2-mongo-svc.yaml
	kubectl create -f 3-rocketchat-rc.yaml
	kubectl create -f 4-rocketchat-svc.yaml

