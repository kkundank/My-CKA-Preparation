### Creating a CA certificate and siging request | [General certificate]()

- [Generate Keys]()
> openssl genrsa -out ca.key 2048

- [ertificate Signing Request]()
> openssl req -new -key ca.key -subj "/CN=KUBERNETES-CA" -out ca.csr

- [Sign Certificates]()
> openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt

### Admin certificate Creation | [Client Certificate]()
> openssl genrsa -out admin.key 2048

> openssl req -new -key admin.key -subj "/CN=kube-admin" -out admin.csr

> openssl x509 -req -in admin.csr -CA ca.crt -CAkey ca.key -out admin.crt

Admin prvileges: Uniquely identifying the admin, by adding this to System-masters group.

> openssl req -new -key admin.key -subj "/CN=kube-admin/O=system:masters" -out admin.csr

Similarly we can create client certificate for kube-scheduler, kube-controller-manager, kube-proxy
Only difference is add a prefix system-kube-scheduler and system-kube-controller-manager for control plane componenets.


### Server certificates

Generate the keys in same ways.
Have multiple keys for HA ETCD cluster.
Define the path for these certs in etcd manifest file.

For API-SERVER

kubernetes
kubernetes.default
kubernetes.default.svc
kubernetes.default.svc.cluster.local
or by IP 10.0.0.0

> openssl genrsa -out apiserver.key 2048

Specifiy a conf file for all DNS and Ip values.
> openssl req -new -key apiserver.key -subj "/CN=kube-apiserver" -out apiserver.csr -config openssl.cnf

> openssl x509 -req -in apiserver.csr -CA ca.crt -CAkey ca.key -out apiserver.crt

For KUBELET

created with node name.

Node names are to be added to group system nodes.
