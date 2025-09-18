這個 Repo 是 [![GitHub Repo](https://img.shields.io/badge/GitHub-Docker--Compose--Sample-181717?logo=github)](https://github.com/rena311706015/Docker-Compose-Sample) 照著步驟做完後的樣子

測試步驟會改為
1. 啟動 minikube
    
    `minikube start`
    
2. 從本機的 docker 切換到 minikube 的 docker
    
    `eval $(minikube docker-env)`
    
3. build backend 和 frontend 的 image 供 minikube 使用
    
    `docker build -t backend ./backend`
    
    `docker build -t frontend ./frontend`
    
4. 為 HPA 啟用 metrics-server
    
    `minikube addons enable metrics-server`
    
5. 啟用 ingress
    1. `minikube addons enable ingress`
    2. `minikube ip` 複製 ip 位置後
    3. `sudo nano /etc/hosts` 最底下新增 `<ip> quarkusapp.minikube.local`
6. apply 所有生成的 yaml
    
    `kubectl apply -f .`
    
7. 測試服務
    
    開啟 https://quarkusapp.minikube.local
    
8. 檢查資料庫
    1. `kubectl exec -it <db-pod-name> -- bash`
    2. `mysql -uroot -prootpass myapp`
    3. `SELECT * FROM messages;`
