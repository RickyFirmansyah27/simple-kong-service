#setup instalation kong api gateway
install kong and etc
make plugin and network

install echo sample service

make rate limit and annotate to echo service

set env 
$env:PROXY_IP = "localhost:80"

set invoker for powershell
foreach ($i in 1..6) {
    Invoke-WebRequest -Uri "http://$env:PROXY_IP/echo" -UseBasicParsing -Method Get | Select-Object -ExpandProperty Headers
}

dont forget anotate key-auth to echo service
kubectl annotate service echo konghq.com/plugins=rate-limit-5-min,key-auth --overwrite

after set key-auth, key-secret and key-consume
Invoke-WebRequest -Uri "http://$env:PROXY_IP/echo" -Headers @{ "apikey" = "hello_world" }


#notes
command kubernetes (k8s)

- kubectl get pods 
- kubectl get deployment -A
- kubectl get httproute
- kubctl get svc
- kubctl etc

apply -f = create depl (yaml or conf)

atasi gagal pull
kubectl rollout restart deployment nama-depl

get all kong
kubectl get all -n kong
