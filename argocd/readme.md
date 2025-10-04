# Esse Lab será focado em fazer o deploy de aplicacoes atraves do argocd

## Criar cluster EKS  
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

## INSTALACAO DO ARGOCD
### (OPCAO 1 - Instalacao via helm)
1 - Adicione o repositorio oficial do Argo CD Helm em sua configuração local do Helm
```bash
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
```

2- Crie o namespace argocd
```bash
kubectl create namespace argocd
```

3 - Instale o Argo CD com o Helm
```bash
helm install argo-cd argo/argo-cd --namespace argocd
```

4 - Verifique se os pods do Argo CD estão sendo executados corretamente no namespace argocd
```bash
kubectl get pods -n argocd
```

5 - Para validar se ocorreu tudo certo, execute o comando para expor a porta 8080 da sua maquina
```bash
kubectl port-forward service/argo-cd-argocd-server -n argocd 8080:443
```

6 - Execute o comando abaixo para pegar as credenciais de acesso, usuario default é (admin).

Obs: Nao copie o caracter (%)
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

### (OPCAO 2 - Instalacao via helm)