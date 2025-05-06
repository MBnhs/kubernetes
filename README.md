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

## ⚠️ Atenção: A edição direta de Pods em execução via kubectl edit é uma prática imperativa e geralmente desencorajada em ambientes de produção, pois as alterações não são persistidas e podem ser perdidas em caso de falhas ou recriações.

## 🚧 A Desvantagem da Abordagem Imperativa
Embora a criação imperativa de Pods seja rápida e útil para testes e aprendizado, ela apresenta algumas limitações importantes:

### Falta de Rastreabilidade: Não há um histórico claro das configurações aplicadas ao cluster.
### Estado Não Declarativo: Não há uma definição explícita do estado desejado do cluster, dificultando a reprodução e o gerenciamento.
### Dificuldade de Auditoria: Acompanhar as mudanças e o estado atual do cluster se torna mais complexo.

## ✨ Rumo à Organização: A Abordagem Declarativa
Para superar essas limitações e manter seu ambiente Kubernetes mais organizado, versionado e gerenciável, a abordagem declarativa é a prática recomendada. Com ela, você define o estado desejado dos seus recursos em arquivos de configuração (YAML ou JSON), permitindo um controle mais robusto e consistente do seu cluster. 📂