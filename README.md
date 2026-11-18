# prova2computacaonuvem

<ins>**1. Fundamentos da Computação em Nuvem**</ins>

**Questão 1 - Qual é a diferença entre IaaS e SaaS? Cite um exemplo de utilização de cada modelo.
  Resposta:** O IaaS fornece a infraestrtura básica de TI (servidores, armazenamento e redes) na nuvem, permitindo que você controle os sistemas operacionais e aplicativos
  Exemplo: Alugar instâncias virtuais na Amazon EC2 ou Microsoft Azure para hospedar servidores de aplicação

  O SaaS entrega um aplicativo completo pronto para uso pela internet, gerenciado inteiramente pelo provedor
  Exemplo: Usar o Google Workspace, Gmail ou Microsoft 365 para e-mails e edição de arquivos

**Questão 2 - Uma empresa utiliza servidores próprios e também recursos de um provedor de nuvem pública. Qual modelo de implatação em nuvem essa empresa utiliza?
  Resposta:** Nuvem Hibrida

**Questão 3 - Qual é a principal diferença entre uma máquina virtual e um contêiner?
  Resposta:** A maquina virtual virtualiza o hardware e possui um sistema operacional completo, enquanto o contêiner virtualza apenas a camada do sistema operacional, compartilhando o kernel da máquina host


<ins>**2. Execução da Aplicação com Docker**</ins>

**Evidência 1 - Contêiner em execução**
```  
  root@ubuntu:~$ docker run -d --name comunicado -p 8090:80 nginx:alpine 
  Unable to find image 'nginx:alpine' locally
  alpine: Pulling from library/nginx
  881fc932939e: Pull complete 
  77a3bfea78f5: Pull complete 
  04c3905a997c: Pull complete 
  7cb374baf968: Pull complete 
  4c8c172c6586: Pull complete 
  1dc588c89da1: Pull complete 
  61d8f4c85a74: Pull complete 
  c4f3d97811f6: Pull complete 
  Digest: sha256:0563c36f94a6d3ec3584161b77859f740f7e20b4853f52c796a864ce6908e8ea
  Status: Downloaded newer image for nginx:alpine
  d02e1ef51f1e429882cc7b27acb754c7e48476959b30cd39b558dc5ea65e75e1
  root@ubuntu:~$ docker ps
  CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                                     NAMES
  d02e1ef51f1e   nginx:alpine   "/docker-entrypoint.…"   8 seconds ago   Up 8 seconds   0.0.0.0:8090->80/tcp, [::]:8090->80/tcp   comunicado
```

**Evidência 2 - Página Personalizada**
```
  root@ubuntu:~$ docker exec comunicado sh -c 'echo "<h1>Comunicado</h1><p>Aluno:                    
  Joao Pedro</p>" > /usr/share/nginx/html/index.html'
  root@ubuntu:~$ curl http://localhost:8090
  <h1>Comunicado</h1><p>Aluno: Joao Pedro</p>
```

<ins>**6. Interpretação dos Resultados**</ins>

**Questão 1 - Qual é a diferença entre uma imagem docker e um contêiner em execução?
  Resposta:** A imagem do Docker funciona como um molde estatico ou uma "planta baixa" que empacota o código e todas as dependências necessarias. O contêiner por sua vez, é a instância ativa rodando a partir dessa imagem atuando como o ambiente em tempo de execução onde a aplicação de fato acontece

**Questão 2 - Qual é a função de um Deployment no Kubernetes?
  Resposta:** O Deployment atua como um controlador que gerência o ciclo de vida e a estabilidade dos Pods. A principal função dele é garantir que o estado desjado da aplicação seja mantido; por exemplo, se um Pod falha ou cai o Deployment automaticamente cria denovo uma nova instância para suprir a ausência e manter o volume de réplicas estipulado

**Questão 3 - O que aconteceu quando você excluiu um Pod? Por que isso aconteceu?
  Resposta:** Quando o Pod foi deletado o cluster não deixou a aplicação desguarnecida: ele imediatamente subiu uma nova instância. Esse comportamento automático aconteceu porque o objeto de Deployment estava configurado para manter o limite de 3 réplicas ativas.

**Questão 4 - Qual é a finalidade de um Service no Kubernets?
  Resposta:** O Service serve como uma camada de abstração de rede dentro do cluster. Ele é o componente responsável por padronizar e tornar possivel a comunicação e o acesso para os Pods, fazendo com que eles possam ser alcançados de forma confiável.

<ins>**7. Conclusão**</ins>

Durante a atividade prática, foi possível compreender a dinamica inicial de criação e customização de ambientes com Docker, incluindo a alteração de arquivos de conteúdo em imagens personalizadas. Alem disso a experiência com o Kubernetes permitiu visualizar na prática conceitos fundamentais de orquestração, como a configuração de Deployments, o gerenciamento de múltiplas réplicas e a resiliência automatizada do cluster frente a falhas ou exclusões de instâncias.

  
