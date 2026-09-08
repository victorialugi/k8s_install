# Домашнее задание «Установка Kubernetes» — Лугинина Виктория
Кластер установлен через kubeadm.

Состав: 1 master + 4 worker.

CRI: containerd.

etcd запущен на master.

## Подготовка нод
На всех нодах отключен swap, включены модули overlay и br_netfilter, включен ip_forward, установлен containerd с SystemdCgroup = true, установлены kubeadm, kubelet, kubectl версии 1.33.

## Инициализация master
sudo kubeadm init --kubernetes-version=v1.33.13 --apiserver-advertise-address=<MASTER_INTERNAL_IP> --pod-network-cidr=10.244.0.0/16

## Сеть подов
Установлен Flannel.
kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml

Манифест: https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml

## Подключение worker
sudo kubeadm join <MASTER_INTERNAL_IP>:6443 --token  --discovery-token-ca-cert-hash sha256:

## Результат
kubectl get nodes -o wide

![1.png](https://github.com/victorialugi/k8s_helm/blob/main/2.png)
