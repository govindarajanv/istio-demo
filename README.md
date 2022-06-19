# istio-demo
wget https://github.com/istio/istio/releases/download/1.0.6/istio-1.0.6-linux.tar.gz
    3  tar -xvf istio-1.0.6-linux.tar.gz
    4  export PATH=$PWD/istio-1.0.6/bin:$PATH
    5  sed -i 's/LoadBalancer/NodePort/;s/31380/30080/' ./istio-1.0.6/install/kubernetes/istio-demo.yaml
    6  kubectl apply -f ./istio-1.0.6/install/kubernetes/istio-demo.yaml
    8  kubectl -n istio-system get pods --watch
   13  kubectl apply -f <(istioctl kube-inject -f istio-1.0.6/samples/bookinfo/platform/kube/bookinfo.yaml)
   16  kubectl apply -f istio-1.0.6/samples/bookinfo/networking/bookinfo-gateway.yaml
   18  kubectl -n istio-system port-forward $(kubectl -n istio-system get pod -l app=grafana -o jsonpath='{.items[0].metadata.name}') 3000:3000 &
   19  sudo apt install -y nginx
   20  vim /etc/nginx/sites-enabled/default
   21  sudo vim /etc/nginx/sites-enabled/default
   ```
   location / {
    # First attempt to serve request as file, then
    # as directory, then fall back to displaying a 404.
    #try_files $uri $uri/ =404;
    proxy_pass http://127.0.0.1:3000;
}
```
   28  sudo nginx -t
   29  sudo systemctl restart nginx
   30  kubectl apply -f ./istio-1.0.6/install/kubernetes/istio-demo.yaml
   Grafana: http://IP ADDRESS/dashboard/db/istio-mesh-dashboard
   BookInfo: http://IP ADDRESS:30080/productpage
