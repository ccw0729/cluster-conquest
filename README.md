# Cluster Conquest

[中文](#中文) · [English](#english)

**線上試玩 / Play online:** https://ccw0729.github.io/cluster-conquest/

**10 秒預告片 / 10-second trailer:** [cluster-conquest.mp4](cluster-conquest.mp4)

---

## 中文

用像素戰略地圖來玩 Kubernetes：城池是 Node，士兵是 Pod，kube-scheduler 是你的軍師。

### 可以玩什麼

- **點城池** 查看節點狀態，可以 cordon、drain、雷擊（NotReady）或重建。
- **排程器面板** 即時顯示 Queue → Filter → Score → Bind，以及每個節點被過濾的原因（taint、NotReady、Insufficient cpu）。
- **流量洪峰** 觸發 HPA 自動擴容。
- **NetworkPolicy** 開啟後，web 直連 db 的封包會被擋下。
- **擴建城池** 加入新的 worker 節點，最多 6 個。
- **kubectl 主控台** 可以直接輸入指令，`oc` 也通用。

### 指令範例

```
kubectl get pods -o wide
kubectl scale deploy/api --replicas=6
kubectl drain worker-1
kubectl describe node worker-2
kubectl create deployment cache --replicas=4 --cpu=1000m
kubectl apply -f netpol.yaml
chaos kill worker-2
```

輸入 `help` 可看完整指令清單。`chaos kill` / `chaos revive` 是沙盤專用指令。

### 說明

- 時間經過壓縮：真實叢集中節點失聯到 Pod 被驅逐約需 5 分鐘（node-monitor-grace-period 加上 toleration），沙盤裡只要 1.6 秒。
- 排程評分是簡化版：`score = 70 × 空閒 CPU 比例 + 30 × 同部隊分散程度`。
- control-plane 帶有 `NoSchedule` taint，所以 Pod 不會被排到王城。
- 整個沙盤是單一 HTML 檔，不需要後端，下載後用瀏覽器直接開啟也能玩。

---

## English

Kubernetes as a pixel-art strategy map: castles are Nodes, soldiers are Pods, and kube-scheduler is your general.

### What you can do

- **Click a castle** to inspect a node, then cordon, drain, strike it with lightning (NotReady), or rebuild it.
- **Scheduler panel** shows Queue → Filter → Score → Bind live, including why each node was filtered out (taint, NotReady, Insufficient cpu).
- **Traffic surge** triggers the HPA to scale out.
- **NetworkPolicy** blocks direct web → db packets when enabled.
- **Expand** adds new worker nodes, up to 6.
- **kubectl console** accepts real commands; `oc` works too.

### Example commands

```
kubectl get pods -o wide
kubectl scale deploy/api --replicas=6
kubectl drain worker-1
kubectl describe node worker-2
kubectl create deployment cache --replicas=4 --cpu=1000m
kubectl apply -f netpol.yaml
chaos kill worker-2
```

Type `help` for the full command list. `chaos kill` / `chaos revive` are sandbox-only commands.

### Notes

- Time is compressed: in a real cluster, evicting pods from an unreachable node takes about 5 minutes (node-monitor-grace-period plus tolerations). Here it takes 1.6 seconds.
- Scheduling is simplified: `score = 70 × free CPU ratio + 30 × spread across the same deployment`.
- The control-plane carries a `NoSchedule` taint, so pods never land in the citadel.
- The whole sandbox is a single HTML file with no backend. Download it and open it in a browser to play offline.

> The in-app interface is in Traditional Chinese; kubectl commands and output are in English.
