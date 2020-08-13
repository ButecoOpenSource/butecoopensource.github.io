---
layout: post
title: Kubernetes explicado
date: 2020-08-13 08:00:00
categories: Desenvolvimento
tags:
  - Container
  - Linux
  - Docker
  - Kubernetes
  - PaaS
permalink: kubernetes-explicado
author: alexandrevicenzi
header:
  overlay_color: "#333"
  show_overlay_excerpt: false
  image: /assets/content/k8s-logo.png
---

O [Kubernetes][kubernetes-io] (K8s) é uma plataforma para orquestrar, gerenciar e escalar containers. A Google criou o projeto inicialmente para uso interno, e tornou-o software livre em 2014.

Com o Kubernetes é possível:

* Escalar aplicações horizontalmente e verticalmente
* Fazer balanceamento de carga
* Fazer descoberta de serviços
* Orquestrar armazenamento
* Executar *rollouts* e *rollbacks* de forma automatizada
* Gerenciar configurações e chaves 
* E muito mais

O Kubernetes não é um PaaS (Platform as a Service), porém ele provê algumas das funcionalidades, como gerenciamento de *deploys*, balanceamento de carga, log e monitoração.

## Conceitos

![Componentes do Kubernetes](/assets/content/components-of-kubernetes.png)

### Cluster

Quando você instala Kubernetes você tem um cluster.

Um cluster geralmente contém múltiplas máquinas. Para o Control Plane o ideal é alta disponibilidade, e para isso é necessário possuir pelo menos dois *master node*. Para a execução de suas aplicações, irá depender do tamanho do seu projeto, mas o ideal também é dois *worker node*, totalizando quatro máquinas.

Em casos mais específicos é possível criar um cluster Kubernetes com apenas uma máquina, ou até mesmo utilizando um Raspberry Pi.

### Pod

Um [Pod][pod], em resumo, é uma instância da sua aplicação no cluster.

[Pod][pod] é o menor objeto no modelo de objetos do Kubernetes. Ele encapsula um ou mais containers, armazenamento, redes e tudo o que for necessário para executar uma aplicação.

### Control Plane

Kubernetes Control Plane garante que o estado atual do cluster é o estado desejado e definido. Para tal, ele executa uma variedade de tarefas automaticamente, inspecionado o cluster e corrigindo qualquer não conformidade.

O Control Plane consiste em um ou mais Kubernetes Master.

### Kubernetes Master

Kubernetes Master, também referido como Master Node, é responsável por manter o cluster no estado desejado, garantindo que todas as aplicações tenham os recursos necessários para sua execução.

No master temos os seguintes componentes:

* [kube-scheduler][kube-scheduler] — Responsável por gerenciar os Pods
* [kube-apiserver][kube-apiserver] — Responsável por expor a API do Kubernetes
* [kube-controller-manager][kube-controller-manager] — Responsáveis pelo controle de nodes, replicação, e outros itens
* [cloud-controller-manager][cloud-controller-manager] — Responsável por integrar com provedores cloud (AWS, GCP, Azure)
* [etcd][etcd] — Banco de dados *key value* que armazena todas as informações do cluster

### Kubernetes Node

Kubernetes Node, também referido como Worker Node e Compute Machine, é responsável por executar os Pods e prover todo o ambiente necessário para tal.

No node temos os seguintes componentes:

* [kubelet][kubelet] — Agente que está presente em todo *worker node* e é responsável por gerenciar os Pods estão rodando, além de se comunicar com o *master node*
* [kube-proxy][kube-proxy] — Proxy de rede que mantém regras e permite a comunicação com Pods dentro e fora da rede
* Container runtime — Software responsável por executar os containers, alguns suportados pelo Kubernetes são o [Docker][docker], [containerd][containerd] e o [CRI-O][CRI-O]

### Objetos

No Kubernetes existe uma série de abstrações que representam o estado de todo o sistema. Os objetos são responsáveis por especificar como as aplicações, serviços, volumes de armazenamento, redes, permissões e outros itens irão se comportar no seu cluster.

Alguns exemplos de objetos comumente usados são:

* [Namespace][namespace] — Separação lógica de aplicações por ambientes
* [Deployment][deployment] — Define o estado desejado de um Pod, quantidade de réplicas, e mais
* [Service][service] — Expõe sua aplicação como um serviço na rede
* [Ingress][ingress] — Expões sua aplicação para acesso externo, define rotas, balanceamento de carga e mais
* [Volumes][volume] — Abstração do armazenamento de dados da sua aplicação

Esses são só alguns dos objetos, existem vários outros, e alguns possuem várias classes, é impossível cobrir todos nesse artigo.

### Kubernetes API

Serviço que disponibiliza as funcionalidades do Kubernetes através de uma API RESTful. É possível interagir diretamente com a API, porém o meio mais comum é através de ferramentas como o *kubectl*.

### kubectl

Ferramenta de linha de comando (CLI) que permite interagir com a API do Kubernetes. É possível usar o *kubectl* para criar, editar, inspecionar e deletar objetos.

## Distribuições

Existem várias distribuições do Kubernetes, cada uma possui algo em particular que talvez se adéque mais a determinados usos.

Para ser considerada uma distribuição compatível com os padrões da [CNCF][cncf] (Cloud Native Computing Foundation), as distribuições devem passar por uma série de critérios para se tornar uma versão certificada. É possível obter uma lista das distribuições certificadas [aqui][landscape-cncf].

Podemos classificar as distribuições em 4 classes para entender um pouco melhor os diferentes tipos de distribuições.

### Puras

São as distribuições que não modificam ou que deixam para o usuário a definição de vários aspectos da instalação e configuração.

O [Kubernetes da CNCF][kubernetes-io] é o oficial, mas a Canonical também gera suas próprias compilações sem modificações.

### Customizadas

São distribuições baseadas na oficial, geralmente entregando uma versão mais fácil de gerenciar ou com funcionalidade não disponível nas versões puras.

A distribuição customizada mais popular é o [OpenShift / OKD][okd-io].

### Limitadas

São as distribuições que possuem uso limitado e específico, geralmente são versões que removem algumas funcionalidades da versão oficial para permitir o uso em certos dispositivos, alguns exemplos são:

* [minikube][minikube] — Kubernetes local
* [MicroK8s][microk8s] — Kubernetes mais leve e de fácil instalação
* [K3s][k3s] — Kubernetes para IoT e embarcados

### Kubernetes as a Service

São as distribuições que são fornecidas por diferentes provedores, geralmente elas integram facilmente com outros produtos e serviços, alguns exemplos são:

* [Azure AKS][azure-aks]
* [Amazon EKS][amazon-eks]
* [Google GKE][google-gke]

## Conclusão

Kubernetes é um assunto extenso, porém é relativamente fácil entender o seu funcionamento. Eu diria que se você já é familiarizado com containers, Docker, Docker Swarm e afins, a curva de aprendizado é relativamente moderada.

Minha recomendação de leitura são os livros [Cloud Native DevOps With Kubernetes][cloud-native-devops-with-kubernetes] e [Kubernetes Up and Running][kubernetes-up-and-running]. Confira como conseguir esses livros gratuitamente [aqui][livros-gratuitos-abril-2020].

Iremos trazer mais conteúdo relacionado a Kubernetes, então fique ligado em nosso blog.

Gostou? Ficou alguma dúvida? Deixe um comentário.

**Referências**

[Documentação do Kubernetes][kubernetes-docs]


[pod]: https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/
[kube-scheduler]: https://kubernetes.io/docs/reference/command-line-tools-reference/kube-scheduler/
[kube-apiserver]: https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/
[kube-controller-manager]: https://kubernetes.io/docs/reference/command-line-tools-reference/kube-controller-manager/
[cloud-controller-manager]: https://kubernetes.io/docs/concepts/architecture/cloud-controller/
[etcd]: https://etcd.io/
[kubelet]: https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/
[kube-proxy]: https://kubernetes.io/docs/reference/command-line-tools-reference/kube-proxy/
[docker]: https://docs.docker.com/engine/
[containerd]: https://containerd.io/docs/
[cri-o]: https://cri-o.io/#what-is-cri-o
[namespace]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[deployment]: https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
[service]: https://kubernetes.io/docs/concepts/services-networking/service/
[ingress]: https://kubernetes.io/docs/concepts/services-networking/ingress/
[volume]: https://kubernetes.io/docs/concepts/storage/volumes/
[cncf]: https://www.cncf.io/
[landscape-cncf]: https://landscape.cncf.io/category=certified-kubernetes-distribution,certified-kubernetes-hosted,certified-kubernetes-installer&format=card-mode&grouping=category
[kubernetes-io]: https://kubernetes.io/
[okd-io]: https://www.okd.io/
[minikube]: https://minikube.sigs.k8s.io/docs/
[microk8s]: https://microk8s.io/
[k3s]: https://k3s.io/
[azure-aks]: https://azure.microsoft.com/en-us/services/kubernetes-service/
[amazon-eks]: https://aws.amazon.com/eks
[google-gke]: https://cloud.google.com/kubernetes-engine/
[cloud-native-devops-with-kubernetes]: http://shop.oreilly.com/product/0636920175131.do
[kubernetes-up-and-running]: http://shop.oreilly.com/product/0636920223788.do
[livros-gratuitos-abril-2020]: https://www.butecopensource.com.br/livros-gratuitos-abril-2020
[kubernetes-docs]: https://kubernetes.io/docs/home/
