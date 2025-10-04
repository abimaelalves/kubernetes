# Esse Lab será focado em fazer o deploy de aplicacoes atraves do argocd

## KIND 
Usaremos o kind para provisionar o cluster kubernetes localmente, lembre-se que o docker precisa estar em execucao para criar os containers para emular ambiente eks localmente

## Passo a passo
Entre no diretorio:
```bash
cd argocd/
```

Note que no arquivo kind.yaml foi definido a criacao do cluster, para criar o cluster basta executar o comando abaixo:
```bash
kind create cluster --config kind.yaml
```

Execute os comandos abaixo para verificar informacao do seu cluster e os nodes criados
```bash
kubectl get nodes
kubectl cluster-info
```

## Instalacao do argocd
Podemos instalar o argo via helm
```bash
    helm repo add argo https://argoproj.github.io/argo-helm
    helm repo update
```