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

Criar namespace argocd
```bash
kubectl create namespace argocd
```

Instalar Argo CD com helm (se atente ao namespace)
```bash
helm install argo-cd argo/argo-cd --namespace argocd
```

Para validar se ocorreu tudo certo, basta executar o seguinte comando para expor a porta 8080 da sua maquina
```bash
kubectl port-forward service/argo-cd-argocd-server -n argocd 8080:443
```

Execute o comando abaixo para pegar as credenciais de acesso, usuario default é (admin).
Obs: Caso na saida do comando abaixo aparecer um caracter de (%) nao copie ele, apenas copie a senha do caracter (%) para traz
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```