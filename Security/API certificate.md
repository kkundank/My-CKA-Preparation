### API certificate

For any user in Kubernetes cluster:

1. Create a key pair:
    openssl genrsa -out kundan.key 2048

2. Generate a CSR and send it to admin.
    openssl req -new kundan.key -subj "/CN=kundan" -out kundan.csr
    
3. Admin create a CSR object usng manifest defination.
    cat kundan.csr | base64 to request of yaml
    
4. Admin can review/approve/reject
    kubectl get csr
    kubectl certificate approve kundan.csr
    kubectl delete csr kundan.csr
    
    echo "" | base64 --decode
