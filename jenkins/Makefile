status:
	kubectl get rc,svc,pods -o wide

clean:
	kubectl delete rc jenkins
	kubectl delete svc jenkins
	kubectl delete pvc pvcjenkins
	kubectl delete pv pv5gjenkins  

all:
	kubectl create -f 1-jenkins-vol.yaml
	kubectl create -f 2-jenkins-svc.yaml
	kubectl create -f 3-jenkins-rc.yaml
