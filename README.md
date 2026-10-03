# Cluster Conquest

用像素戰略地圖來玩 Kubernetes：城池是 Node，士兵是 Pod，kube-scheduler 是你的軍師。

**線上試玩：** https://ccw0729.github.io/cluster-conquest/

**10 秒預告片：** [cluster-conquest.mp4](cluster-conquest.mp4)

## 可以玩什麼

- **點城池** 查看節點狀態，可以 cordon、drain、雷擊（NotReady）或重建。
- **排程器面板** 即時顯示 Queue → Filter → Score → Bind，以及每個節點被過濾的原因（taint、NotReady、Insufficient cpu）。
- **流量洪峰** 觸發 HPA 自動擴容；**NetworkPolicy** 開啟後，web 直連 db 的封包會被擋下。
- **kubectl 主控台** 可以直接輸入指令，`oc` 也通用：

```
kubectl get pods -o wide
kubectl scale deploy/api --replicas=6
kubectl drain worker-1
kubectl describe node worker-2
kubectl create deployment cache --replicas=4 --cpu=1000m
kubectl apply -f netpol.yaml
chaos kill worker-2
```

輸入 `help` 可看完整指令清單。

## 說明

時間經過壓縮：真實叢集中節點失聯到 Pod 被驅逐約需 5 分鐘（node-monitor-grace-period 加上 toleration），沙盤裡只要 1.6 秒。

整個沙盤是單一 HTML 檔，不需要後端，下載後用瀏覽器直接開啟也能玩。
