# ☸️ Kubernetes

Projeto de estudo! 🚀

## Problemas de disponibilidade, e agora? 🤔

Para lidar com problemas de disponibilidade, podemos considerar duas abordagens principais:

- *Escalabilidade Vertical (Scale Up):* 💪 Adicionar mais poder computacional a uma máquina existente (CPU, memória, disco).
- *Escalabilidade Horizontal (Scale Out):* ➕ Adicionar mais máquinas para trabalharem em paralelo, distribuindo a carga.

## Kubernetes: O Orquestrador de Containers 🤖

O Kubernetes entra em cena para gerenciar um ou mais computadores trabalhando juntos como um *cluster*. Ele simplifica a criação e o gerenciamento desses clusters.

### Autocura e Escalabilidade Inteligente ✨

- *Recuperação Automática:* Se uma máquina falhar e ficar offline, o Kubernetes automaticamente provisiona e adiciona uma nova máquina ao cluster para substituir a anterior. 🛠️
- *Escalonamento Dinâmico:* Quando uma máquina atinge o limite máximo de seu poder de processamento, o Kubernetes pode criar novas máquinas no cluster para lidar com o aumento da demanda. 📈

## Benefícios Chave 🌟

- *Aplicações Mais Escaláveis:* Sua aplicação pode lidar com mais tráfego e carga de trabalho de forma eficiente.
- *Restarts Automatizados:* Em caso de falhas em containers individuais, o Kubernetes os reinicia automaticamente, garantindo maior resiliência.
- *Orquestração de Containers:* Simplifica o gerenciamento e a implantação de aplicações conteinerizadas.

## ⚙️ Recursos do Kubernetes

Explorando os componentes fundamentais que compõem o Kubernetes:

### 🧱 Recursos Primordiais

  - **📦 Pods:** A menor unidade de implantação no Kubernetes, que encapsula um ou mais containers compartilhando recursos.
  - **⚙️ Replica Sets (rs):** Asseguram que um número específico de réplicas de um Pod estejam sempre em execução, promovendo a disponibilidade.
  - **💾 Volumes:** Oferecem armazenamento persistente para os containers dentro de um Pod.
  - **💾💾 Persistent Volumes (PV):** Abstraem o armazenamento físico, permitindo que os Pods consumam armazenamento de forma independente do ciclo de vida dos Pods.

A combinação estratégica desses recursos permite a arquitetura e o gerenciamento eficaz de nossos ambientes no Kubernetes. 🏗️

### 🏢 Arquitetura do Cluster: Master e Nodes

Um cluster Kubernetes é estruturado em dois tipos principais de nós:

#### 🧠 Master Node (Painel de Controle)

O Master atua como o centro de controle do cluster, responsável por gerenciar seu estado e tomar decisões sobre a execução dos containers. Seus componentes chave incluem:

  - **🗣️ kube-apiserver:** A interface primária para interagir com o cluster Kubernetes.
  - **⚙️ kube-controller-manager:** Executa controladores que regulam o estado do cluster.
  - **🗓️ kube-scheduler:** Determina em qual nó executar novos Pods.
  - **🔑 etcd:** Um armazenamento de chave-valor distribuído para os dados de configuração do cluster.

A comunicação com o Master é realizada principalmente através da ferramenta de linha de comando **kubectl**. ⌨️

`kubectl` oferece duas formas de interação com o cluster:

  - **📜 Declarativa:** Definindo o estado desejado em arquivos de configuração (YAML/JSON).
  - **🚀 Imperativa:** Executando comandos diretos para realizar ações específicas.

#### 🛠️ Worker Nodes (Nós de Trabalho)

Os Nodes são as máquinas onde as aplicações são efetivamente executadas. Cada Node integra os seguintes componentes essenciais:

  - **🧑‍🔧 kubelet:** Um agente que garante que os containers definidos nos Pods estejam em execução.
  - **🌐 kube-proxy:** Um proxy de rede que implementa as regras de rede do Kubernetes.

A colaboração entre o Master e os Nodes estabelece a base para um gerenciamento eficiente e a escalabilidade das aplicações no Kubernetes. 💪


# 📦 Entendendo os Pods no Kubernetes

## 🤔 Do Docker para o Kubernetes: Uma Nova Abstração

No universo do Docker, a unidade fundamental de manipulação são os **containers**. Já no Kubernetes, o conceito central evolui para o **Pod**.

## 🚀 O Que é um Pod? Uma Cápsula de Containers

Um Pod pode ser imaginado como uma **cápsula** que tem a capacidade de conter um ou mais **containers** em seu interior. Essa é uma diferença crucial na forma como as aplicações são organizadas e gerenciadas.

### 🛠️ Interagindo com o Kubernetes: Criando Pods

Ao utilizarmos a ferramenta de linha de comando `kubectl` para interagir com o Kubernetes, a ação primária é a criação de um **Pod**, e não diretamente de um container. É importante lembrar que este Pod pode abrigar um único ou múltiplos containers, dependendo da necessidade da sua aplicação.

## 🔄 O Que Muda com os Pods?

### 🌐 Endereçamento de Rede: IP no Nível do Pod

Uma mudança significativa é o tratamento do endereço IP. Ao criar um Pod, ele recebe um **endereço IP único**. Isso significa que o endereço IP não está mais associado diretamente ao container individual, mas sim ao Pod como um todo.

### 🚪 Mapeamento de Portas Dentro do Pod

Dentro do contexto de um Pod, é possível realizar o mapeamento das portas atribuídas ao seu endereço IP. Por exemplo, ao fazer uma requisição para o IP do Pod na porta `8080`, essa requisição será direcionada ao container que está escutando na porta `8080` dentro desse Pod. O mesmo princípio se aplica a outros containers rodando em portas diferentes dentro do mesmo Pod (ex: porta `9000`). Eles compartilham o mesmo IP, mas cada um opera em sua própria porta.

## ⚙️ Capacidades Adicionais dos Pods

### ⚠️ Resiliência de Containers Singulares

Se um Pod contém apenas um container e esse container para de funcionar, o Pod também é considerado inativo. No entanto, o Kubernetes possui a capacidade de **recriar automaticamente um novo Pod**, que receberá um novo endereço IP. Essa característica torna os Pods inerentemente **efêmeros**: eles podem ser destruídos e recriados a qualquer momento, e um novo Pod não terá nenhuma relação com o Pod anterior.

### 💪 Resiliência em Pods Multi-Container

Em cenários onde um Pod hospeda dois ou mais containers, se um desses containers falhar, o Pod em si permanece ativo. O Kubernetes então se encarrega de criar um novo container para substituir aquele que falhou, mantendo os demais containers em execução dentro do mesmo Pod.

## 🔗 Redes e Compartilhamento Dentro do Pod

### 🤝 Compartilhamento de Recursos

Os containers que residem dentro do mesmo Pod compartilham o mesmo endereço IP e, consequentemente, os mesmos namespaces de rede e IPC (Inter-Process Communication). Além disso, eles também têm a capacidade de compartilhar **volumes de armazenamento**.

### 🗣️ Comunicação Localhost

Devido ao compartilhamento do mesmo endereço IP, os containers dentro de um Pod podem se comunicar diretamente entre si utilizando o `localhost`. Essa proximidade facilita a interação e o compartilhamento de dados entre processos relacionados que compõem uma unidade lógica de aplicação.


# 🚀 Criando Pods de Forma Imperativa no Kubernetes

## ⚙️ Preparando o Terreno: Iniciando o Minikube

Antes de começarmos a criar nossos Pods, é fundamental ter um cluster Kubernetes em execução. Para ambientes de desenvolvimento local, o **Minikube** é uma excelente ferramenta.

```bash
minikube start
```

Este comando irá iniciar sua instância local do Kubernetes. 🚦

## 🛠️ kubectl: Seu Canivete Suíço do Kubernetes
A ferramenta kubectl é a sua principal interface para interagir com o cluster Kubernetes. Com ela, você pode criar, ler, atualizar e remover diversos recursos dentro do seu cluster.

## 🏃‍♀️ Criando seu Primeiro Pod com kubectl run
O comando kubectl run é utilizado para criar um novo Pod de maneira rápida e direta. Ele aceita alguns parâmetros essenciais:

O primeiro parâmetro define o nome que você deseja dar ao seu Pod.
O segundo parâmetro, precedido por --image=, especifica o nome da imagem do container que será executada dentro do Pod.

## 🐳 Exemplo Prático: Criando um Pod do Nginx
Para criar um Pod que execute o servidor web Nginx, utilizando a última versão da imagem, execute o seguinte comando:

```bash
kubectl run nginx-pod --image=nginx:latest
```

## 👀 Visualizando os Pods Criados com kubectl get pods
Após executar o comando de criação, você pode verificar o status dos seus Pods utilizando o seguinte comando:


```bash
kubectl get pods
```

Este comando listará todos os Pods em execução no seu namespace atual, mostrando informações como nome, status e há quanto tempo estão rodando.

## 👀 Acompanhando a Criação com --watch
Para acompanhar em tempo real o processo de criação e as mudanças de status dos seus Pods, você pode adicionar a flag --watch ao comando kubectl get pods:

```bash
kubectl get pods --watch
```
Isso manterá sua tela atualizada com as informações dos Pods conforme eles são criados e mudam de estado. 📺

## 🔍 Detalhes do Pod: Investigando com kubectl describe pod
Para obter informações mais detalhadas sobre um Pod específico, incluindo os eventos de criação, configuração e status dos containers dentro dele, utilize o comando kubectl describe pod seguido do nome do Pod:

```bash
kubectl describe pod nome-do-pod
```

Este comando fornecerá um panorama completo do ciclo de vida e da configuração do seu Pod. 🧐

## ✏️ Modificando a Configuração de um Pod com kubectl edit pod
Caso necessite alterar alguma configuração de um Pod existente, você pode utilizar o comando kubectl edit pod seguido do nome do Pod:

```bash
kubectl edit pod nome-do-pod
```

 **⚠️ Atenção: A edição direta de Pods em execução via kubectl edit é uma prática imperativa e geralmente desencorajada em ambientes de produção, pois as alterações não são persistidas e podem ser perdidas em caso de falhas ou recriações**.

## 🚧 A Desvantagem da Abordagem Imperativa
Embora a criação imperativa de Pods seja rápida e útil para testes e aprendizado, ela apresenta algumas limitações importantes:

- **Falta de Rastreabilidade:** Não há um histórico claro das configurações aplicadas ao cluster.
- **Estado Não Declarativo:** Não há uma definição explícita do estado desejado do cluster, dificultando a reprodução e o gerenciamento.
- **Dificuldade de Auditoria:** Acompanhar as mudanças e o estado atual do cluster se torna mais complexo.

## ✨ Rumo à Organização: A Abordagem Declarativa
Para superar essas limitações e manter seu ambiente Kubernetes mais organizado, versionado e gerenciável, a abordagem declarativa é a prática recomendada. Com ela, você define o estado desejado dos seus recursos em arquivos de configuração (YAML ou JSON), permitindo um controle mais robusto e consistente do seu cluster. 📂


# 📝 Criando Pods de Forma Declarativa no Kubernetes

## 📄 Definição de Recursos: JSON ou YAML?

Ao trabalhar com a abordagem declarativa no Kubernetes, as configurações dos seus recursos, como os Pods, são definidas em arquivos. Esses arquivos podem ser formatados em **JSON** (`.json`) ou **YAML** (`.yaml`). Embora ambos sejam válidos, o formato **YAML** é geralmente preferido por sua sintaxe mais limpa e legível para humanos. 👍

## 🧱 Estrutura Básica de um Arquivo de Definição de Pod (YAML)

Um arquivo de definição de Pod em YAML tipicamente contém as seguintes seções principais:

```yaml
apiVersion: # Versão da API do Kubernetes
kind:       # Tipo do recurso a ser criado
metadata:   # Metadados do recurso
spec:       # Especificações do recurso
```

Vamos detalhar cada uma dessas seções:

## apiVersion: A Versão da API 🏷️

Este campo especifica a versão da API do Kubernetes que você está utilizando para criar o recurso. Ao utilizar o prefixo "v", como em v1, indica que você está trabalhando com uma versão estável da API.

```yaml
apiVersion: v1
```

## kind: O Tipo de Recurso 📌
Aqui, você define o tipo de recurso que deseja criar. No nosso caso, para criar um Pod, o valor deste campo será Pod.

```yaml
kind: Pod
```

## metadata: Informações Adicionais ℹ️
Esta seção contém metadados sobre o Pod, como o seu nome (name), que é um identificador único dentro do namespace.

```yaml
metadata:
  name: meu-primeiro-pod
```

## spec: As Especificações do Pod ⚙️
A seção spec define as especificações desejadas para o Pod. Um dos campos mais importantes dentro de spec é containers, que é uma lista de definições de containers que serão executados dentro do Pod. Cada container requer um name (nome do container) e uma image (a imagem Docker a ser utilizada).

```yaml
spec:
  containers:
  - name: meu-container
    image: nginx:latest
```

## 🚀 Aplicando o Arquivo de Definição com kubectl apply
Para que o Kubernetes crie o Pod com base no seu arquivo de definição, você utiliza o comando kubectl apply seguido da flag -f (para "file") e o nome do seu arquivo (por exemplo, primeiro-pod.yaml).

```yaml
kubectl apply -f primeiro-pod.yaml
```

## ✨ Foco na Declaração, Poder na API
Ao adotar a abordagem declarativa, nosso foco se desloca para a entrega de um arquivo de definição claro e conciso para o Kubernetes. A API do Kubernetes então assume a responsabilidade de interpretar essa definição e provisionar os Pods conforme especificado. Isso simplifica o gerenciamento e promove a consistência do seu ambiente. 🎯


## 🚀 Iniciando o Projeto

🧹 Limpeza Inicial

Antes de tudo, vamos dar uma faxina e remover quaisquer pods rodando por aí.

```bash
# Para deletar um pod criado na correria (imperativo):
kubectl delete pod nome-do-pod

# Para deletar pods definidos em um arquivo (declarativo):
kubectl delete -f ./nome-do-arquivo-onde-estao-declarados-os-pods.yaml
```

## 📰 Nosso Cenário: Portal de Notícias

Vamos botar a mão na massa com um portal de notícias!


## ✍️ Criando o arquivo portal-noticias.yaml:

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: portal-noticias
spec:
    containers:
        - name: portal-noticias-container
          image: aluracursos/portal-noticias:1
```


## ⚙️ Aplicando a configuração:

```bash
kubectl apply -f ./portal-noticias.yaml
```


## 🌐 Acessando no Navegador

Para dar uma espiada no nosso portal, precisamos do IP do pod:
```bash
kubectl describe pod portal-noticias
```

Abra seu navegador e digite o IP obtido, seguido da porta 8080 (ex: http://<IP>:8080).


## 🕵️‍♀️ Investigando Problemas
Ops! Parece que o site não está abrindo como esperado. Vamos investigar mais a fundo! Podemos entrar na linha de comando do pod assim:

```bash
kubectl exec -it portal-noticias -- bash
```

```bash
curl localhost
```

🤔 Vemos que as informações estão lá dentro. Isso significa que o problema é que estamos acessando o IP do pod, e não diretamente o IP do nosso container com a aplicação.


## 💡 Próximo Passo: Expor o Container

Para que o nosso portal seja acessível externamente, precisaremos "expor" o container.



## 🚀 Comunicação entre Pods com Services no Kubernetes
A comunicação entre pods em um cluster Kubernetes é um conceito fundamental para o funcionamento de aplicações distribuídas. Embora seja possível a comunicação direta via IP, a natureza efêmera dos pods (seus IPs podem mudar em caso de reinício) torna essa abordagem inviável para um sistema robusto. É aí que entram os Services (ou SVCs).


## 🌐 O que são Services?
Services são abstrações que expõem aplicações rodando em um ou mais pods, provendo IPs fixos e DNS para esses pods. Isso significa que, em vez de um pod se comunicar diretamente com o IP de outro pod, ele se comunica com o DNS do Service. Além de estabilidade, os Services também podem atuar como balanceadores de carga, distribuindo as requisições entre os pods associados.

Em resumo, a comunicação ideal é feita através do DNS do Service, e não diretamente pelo IP do pod.

## 🚦 Tipos de Services
Existem três tipos principais de Services:

ClusterIP: 🏡 Para comunicação interna entre pods dentro do mesmo cluster.
NodePort: 🚪 Expõe um Service na porta de cada Node do cluster, permitindo acesso externo.
LoadBalancer: ⚖️ Cria um LoadBalancer externo (se o ambiente de cloud suportar) para expor o Service.

## 🏘️ ClusterIP
O ClusterIP é ideal para comunicação interna entre diferentes pods dentro do mesmo cluster. Um pod com um Service do tipo ClusterIP pode ser acessado por outros pods dentro do cluster. No entanto, é importante notar que um pod só pode ser acessado por outros se houver um Service que o exponha; o inverso não é verdadeiro (um pod sem Service não pode ser acessado diretamente por outros pods a partir de fora do cluster). O ClusterIP não permite acesso externo ao cluster.

## Exemplo de ClusterIP
Para demonstrar o ClusterIP, vamos criar dois pods e um Service:

Pod 1:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-1
spec:
  containers:
    - name: container-pod-1
      image: nginx:latest
      ports:
        - containerPort: 80
```


Pod 2

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-2
spec:
  containers:
    - name: container-pod-2
      image: nginx:latest
      ports:
        - containerPort: 80
```

Para vincular o svc-pod-2 ao pod-2, adicionamos a label app: segundo-pod ao yaml do pod-2.

Service do Pod 2:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: servicec-pod-2
spec:
  type: ClusterIP
  selector:
    app: segundo-pod
```


A seção ports define a porta do Service (port: 80) e para qual porta do pod ele irá direcionar as requisições (se não especificado targetPort, assume a mesma porta do port).

## 🧪 Testando a Comunicação
Obter o IP do Service:

```bash
kubectl get svc
```

Acessar o Pod 1:
```bash
kubectl exec -it pod-1 -- bash
```

Acessar o Service pelo IP:
```bash
curl {ip-do-service}:8080
```

Você também pode acessar o Service pelo seu DNS (o nome do Service é o DNS dentro do cluster).

## 🎯 Redirecionamento de Portas
Se a porta exposta pelo Service for diferente da porta de acesso do pod vinculado, você pode definir a porta alvo com targetPort:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: servicec-pod-2
spec:
  type: ClusterIP
  selector:
    app: segundo-pod
  ports:
   - port: 80
     targetPort: 9000
```


Nesse caso, o comando curl seria:

```bash
curl {ip-do-service}:9000
```