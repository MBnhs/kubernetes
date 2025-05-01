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