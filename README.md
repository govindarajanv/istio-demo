# istio-demo
- wget https://github.com/istio/istio/releases/download/1.0.6/istio-1.0.6-linux.tar.gz
- tar -xvf istio-1.0.6-linux.tar.gz
- export PATH=$PWD/istio-1.0.6/bin:$PATH
- sed -i 's/LoadBalancer/NodePort/;s/31380/30080/' ./istio-1.0.6/install/kubernetes/istio-demo.yaml
- kubectl apply -f ./istio-1.0.6/install/kubernetes/istio-demo.yaml
- kubectl -n istio-system get pods --watch
- kubectl apply -f <(istioctl kube-inject -f istio-1.0.6/samples/bookinfo/platform/kube/bookinfo.yaml)
- kubectl apply -f istio-1.0.6/samples/bookinfo/networking/bookinfo-gateway.yaml
- kubectl -n istio-system port-forward $(kubectl -n istio-system get pod -l app=grafana -o jsonpath='{.items[0].metadata.name}') 3000:3000 &
- sudo apt install -y nginx
- vim /etc/nginx/sites-enabled/default
- sudo vim /etc/nginx/sites-enabled/default
   ```
   location / {
    # First attempt to serve request as file, then
    # as directory, then fall back to displaying a 404.
    #try_files $uri $uri/ =404;
    proxy_pass http://127.0.0.1:3000;
}
```

- sudo nginx -t
- sudo systemctl restart nginx
- kubectl apply -f ./istio-1.0.6/install/kubernetes/istio-demo.yaml
- Grafana: http://IP ADDRESS/dashboard/db/istio-mesh-dashboard
- BookInfo: http://IP ADDRESS:30080/productpage
