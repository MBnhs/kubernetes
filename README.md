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