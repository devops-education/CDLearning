# Introdução

O CDLearning é uma ambiente de apoio ao aprendizado da [Entrega Contínua de Software](https://pt.wikipedia.org/wiki/Entrega_cont%C3%ADnua) (ECS), um dos pilares fundamentais de DevOps. O ambiente lida com desafios de ensino DevOps reportados pela comunidade,  tais  como:  

- promover  a  integração  de  ferramentas  de  ECS  para  diminuir  a carga de trabalho de professores;
- mitigar a dificuldade inicial de configuração de pipeline ECS de projetos através da oferta de configurações iniciais de pipeline que podem ser usados e estendidos pelos estudantes.

## Caso de Uso do Cadastro de um Sistema

O aluno acessa a interface gráfica do Microservico (imagem abaixo), informando o nome do sistema e o endereço do repositório do código fonte a ser criado no Gitlab.

![Adicionando um sistema.]({{site.url}}/images/adicionarServico.png "Cadastrando um sistema.")

O Microservico é um serviço desenvolvido internamente com a finalidade de realizar integração e configuração dos outros serviços utilizados no ambiente. O Gitlab é uma ferramenta de software livre especializada em versionamento de código fonte e gestão de tarefas. No passo 2 da figura abaixo, o Microservico acessa o Gitlab, cria o repositório do código e configura esse serviço para notificar o Jenkins de eventuais alterações no código. O Jenkins é software livre especializado em automação de ECS. No passo 3, o Microservico cria no Jenkins o job que será responsável por executar o pipeline da aplicação recém cadastrada. Por fim, o Microservico configura o Nginx no passo 4, criando uma rota de acesso na internet para a aplicação desenvolvida. O Nginx é um software livre utilizado como proxy reverso de aplicações web.

![Configurando um sistema automaticamente.]({{site.url}}/images/cdlearning_pipeline_cadastro.png "Configurando um sistema automaticamente após cadastro.")

## Caso de Uso do Pipeline de Construção de um Sistema

Durante o desenvolvimento do sistema, a execução da sua respectiva ECS será invocada toda vez que o aluno submeter alteração no código para o Gitlab, conforme ilustra o passo 1 da Figura abaixo. No passo 2, o Gitlab notifica o Jenkins da mudança do código. Por sua vez, o Jenkins executa o pipeline nos passos 3, 4 e 5. No passo 3, o Jenkins executa as tarefas de atualização do código fonte, compilação, análise estática, testes e construção do executável da aplicação. No passo 4, o Jenkins armazena a imagem desse executável no Nexus. O Nexus é um software livre que serve como repositório de artefatos. Por fim, o Jenkins cria o contêiner da aplicação em uma das máquinas virtuais do ambiente de hospedagem a partir da imagem armazenada no Nexus. Dessa forma, ao final da ECS, o aluno verificará a execução de sua aplicação refletindo as modificações realizadas no código fonte. Vale ressaltar que o único trabalho do aluno é indicar o nome do sistema e o endereço do repositório do código fonte a ser criado no Gitlab, conforme descrito anteriormente.

![Executando a Entrega Contínua de Software.]({{site.url}}/images/cdlearning_pipeline.png "Executando a Entrega Contínua de Software.")

## Detalhe de um serviço

No módulo Microservico, é possível acessar detalhes do contêineres, o sistema em um endereço na internet do tipo MeuSistema.devops.xxxx.zz, o repositório do código fonte no Gitlab, as execuções da ECS no Jenkins, a imagem da aplicação no Nexus e gerenciar o acesso de membros do serviço.

![Detalhe de um sistema.]({{site.url}}/images/detalheServico.png "Detalhe de um Sistema / Serviço.")

## Detalhe dos containeres de um serviço

No módulo Microservico, é possível visualizar a quantidade dos contêineres, portas, volumes, imagens e parâmetros de inicialização da execução.

![Detalhe dos conteineres de um Sistema / Serviço.]({{site.url}}/images/detalheContaineres.png "Detalhe dos conteineres de um Sistema / Serviço.")

## Arquitetura Geral do CDLearning

O ambiente disponibiliza os seguintes serviços:

- Serviço de Repositório de Código Fonte ([GitLab](https://about.gitlab.com/))
- Serviço de Execução de _Pipeline_ ([Jenkins](https://www.jenkins.io/))
- Serviço de Armazenamento de Artefatos ([Nexus](https://www.sonatype.com/))
- Serviço de Conteinização ([Docker](https://www.docker.com/))
- Serviço de Gerenciamento de Configuração ([Ansible](https://www.ansible.com/))

![Arquitetura da solução CDLearning.]({{site.url}}/images/arquiteturaDevOps.png "Arquitetura da solução CDLearning.")

## Quem usa o CDLearning

Atualmente, o CDLearning está em operação no IFRN (Instituto Federal do Rio Grande do Norte) no endereço ([DevOps IFRN](https://devops.ifrn.edu.br/))
