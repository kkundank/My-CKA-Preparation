### View a certificate

cat /etc/kubernetes/manifests/kube-api-server.yaml

Then check for apiserver path and open

openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout

journalctl -u etcd.service -l

kubectl logs etcd-master

docker ps

docker logs container_id

openssl x509 -req -in /etc/kubernetes/pki/apiserver-etcd-client.csr 
-CA /etc/kubernetes/pki/etcd/ca.crt -CAkey /etc/kubernetes/pki/etcd/ca.key 
-CAcreateserial -out /etc/kubernetes/pki/apiserver-etcd-client.crt
