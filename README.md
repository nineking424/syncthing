# Syncthing Kubernetes Deployment

Syncthing을 Kubernetes에 배포하기 위한 매니페스트 파일 모음입니다.

Syncthing은 오픈소스 P2P 파일 동기화 도구로, 여러 기기 간에 파일을 안전하게 동기화할 수 있습니다.

---

Kubernetes manifests for deploying Syncthing.

## Components

| File | Description |
|------|-------------|
| `namespace.yaml` | syncthing namespace |
| `pvc.yaml` | PersistentVolumeClaims (config: 1Gi, data: 10Gi) |
| `deployment.yaml` | Syncthing pod deployment |
| `service.yaml` | LoadBalancer service |

## Ports

| Port | Protocol | Description |
|------|----------|-------------|
| 8384 | TCP | Web UI |
| 22000 | TCP/UDP | Sync protocol |
| 21027 | UDP | Local discovery |

## Deploy

```bash
kubectl apply -f .
```

## Access

After deployment, get the LoadBalancer IP:

```bash
kubectl get svc -n syncthing
```

- **Web UI**: `http://<EXTERNAL-IP>:8384`
- **Sync**: `tcp://<EXTERNAL-IP>:22000`

## Data Paths

| Mount Path | Description |
|------------|-------------|
| `/var/syncthing/config` | Configuration files |
| `/var/syncthing/data` | Synchronized data |

## Configuration

Environment variables in deployment:

| Variable | Value | Description |
|----------|-------|-------------|
| `PUID` | 1000 | User ID |
| `PGID` | 1000 | Group ID |
| `TZ` | Asia/Seoul | Timezone |
