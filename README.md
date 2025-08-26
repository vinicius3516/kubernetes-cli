# Kubernetes Pods & Images CLI

Uma CLI em Python para listar **pods** e suas respectivas **imagens Docker** em clusters Kubernetes.

Permite filtrar por **namespaces**, exibindo os resultados em uma tabela formatada com cores para melhor visualização.

Este projeto foi desenvolvido como parte de um curso de Python aplicado a DevOps e pode ser usado como ferramenta de apoio para inspeção rápida de workloads em clusters Kubernetes.

---

> ## Funcionalidades

- Listar **todos os pods** de todos os namespaces.
- Filtrar pods e imagens por **namespace específico**.
- Saída formatada em **tabela** (via [tabulate](https://pypi.org/project/tabulate/)).
- Uso de **cores** para melhor leitura (via [colorama](https://pypi.org/project/colorama/)).

---

> ## Tecnologias Utilizadas

- [Python 3](https://www.python.org/)
- [Kubernetes Client](https://github.com/kubernetes-client/python)
- [Tabulate](https://pypi.org/project/tabulate/)
- [Colorama](https://pypi.org/project/colorama/)

---

> ## Instalação

### Subindo um cluster Kind (local)

**Requisitos: Docker, kubectl, kind.**


```bash
# 1) Clone este repositório
git clone https://github.com/vinicius3516/kubernetes-cli.git
cd kubernetes-cli

# 2) Criar o cluster usando o config.yaml deste repositório
kind create cluster --name kubernetes-cli --config config.yaml

# 3) Verificar contexto e nós
kubectl cluster-info
kubectl get nodes -o wide

# 4) (Opcional) Aplicar o deployment de teste (nginx)
kubectl apply -f deployment.yaml

# 5) Rodar a CLI
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python kube-get-images.py
```

> ## Uso

### Listar todos os pods de todos os namespaces:

```bash
python kube-get-images.py
```

### Listar pods de um namespace específico:

```bash
python kube-get-images.py -n default
```

---

> ## Exemplo de Saída

**Todos os namespaces:**

```
+--------------------------------------------+-------------------------------------------------------------+
| Pods                                       | Images                                                      |
+============================================+=============================================================+
| nginx-deployment-55f5468b79-krqcq          | nginx                                                       |
| coredns-674b8bbfcf-l57ct                   | registry.k8s.io/coredns/coredns:v1.12.0                     |
| kube-apiserver-kind-control-plane          | registry.k8s.io/kube-apiserver:v1.33.1                      |
| local-path-provisioner-7dc846544d-r4vz5    | docker.io/kindest/local-path-provisioner:v20250214-acbabc1a |
+--------------------------------------------+-------------------------------------------------------------+

```

**Namespace filtrado (`default`):**

```
+-----------------------------------+----------+
| Pods                              | Images   |
+===================================+==========+
| nginx-deployment-55f5468b79-krqcq | nginx    |
+-----------------------------------+----------+
```

---

> ## Estrutura do Projeto

```
kubernetes-cli/
│── kube-get-images.py     # Script principal da CLI
│── requirements.txt       # Dependências do projeto
│── deployment.yaml        # Deploy do nginx no cluster no -n default
│── config.yaml            # Config do kind para subir um cluster localmente
│── README.md              # Documentação
```