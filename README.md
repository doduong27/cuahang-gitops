# cuahang-gitops — Kho Lưu Trữ Cấu Hình GitOps

Kho lưu trữ Kubernetes manifests cho toàn bộ 3 môi trường của dự án **`cuahang`**.

## Cấu trúc thư mục:
* **`argocd/`**: Khai báo `AppProject` và 3 `Application` (`dev`, `stag`, `prod`).
* **`projects/cuahang/base/`**: Cấu hình Kubernetes dùng chung (Deployment, Service, Ingress, NetworkPolicy).
* **`projects/cuahang/overlays/dev/`**: Đồng bộ tự động (`auto-sync` + `selfHeal`), kết nối `cuahang_dev`.
* **`projects/cuahang/overlays/stag/`**: Đồng bộ tự động, kết nối `cuahang_stag`.
* **`projects/cuahang/overlays/prod/`**: Yêu cầu phê duyệt và bấm **Sync thủ công**, chạy 2 Replicas, kết nối `cuahang_prod`.

## Cách triển khai vào cụm Argo CD:
```bash
# Đứng trên máy 192.168.1.252 (K8s node):
kubectl apply -f argocd/appproject-cuahang.yaml
kubectl apply -f argocd/app-cuahang-dev.yaml
kubectl apply -f argocd/app-cuahang-stag.yaml
kubectl apply -f argocd/app-cuahang-prod.yaml
```
Hoặc tạo ứng dụng trực tiếp từ giao diện Web Argo CD: `https://192.168.1.252:30443`.
