# Arquitetura de um site JAMStack

### A Jamstack é uma arquitetura criada para construir sites estáticos.

### Objetivos

Este documento foi elaborado, com informações básicas sobre como você pode hospedar um site estático, com domínio próprio sem custo de hospedagem, usando Netlify Drop integrado ao Github.

No final desta jornada, teremos uma arquitetura de um site JAMStack, diferente de sites que utilizam um servidor backend tradicional. Nosso site estará hospedado e integrado ao Github, onde você poderá apresentar seus portfólios de trabalhos ou estudos acadêmicos, usando o seu domínio personalizado e com SSL grátis.

### Restrições

- Hospedagem para arquivos HTML, CSS e Javascript;
- Suporte para projetos em ReactJS ou similares;
- Suporte para entrega contínua e/ou à implantação contínua com GitHub (CI/CD).

### Considerações iniciais

Existem várias arquiteturas e possibilidades de hospedagens gratuitas, este documento é mais uma das proposições (sugestões), dentre as excelentes soluções que existem na Internet.

Neste exemplo os arquivos (fontes) HTML, CSS e imagens foram hospedagas no GitHub, e o domínio foi registrado no Registro.br, que é o departamento do NIC.br responsável pelas atividades de registro e manutenção dos nomes de domínios que usam o .br.

### Pré-requisitos

- Registrar ou ter um nome de domínio registrado;
- Acesso administrativo para realizar configurações personalizadas nos serviços de DNS do domínio;
- Cadastro no GitHub (https://github.com/);
- Cadastro no Netlify (https://www.netlify.com)

### Introdução

JAMStack (sites estáticos) é uma técnica para criar sites e aplicativos que oferecem bom desempenho, segurança e excelente custo de escala.

Arquitetura JAMStack consiste em sites com a seguinte estrutura:

- JavaScript
- APIs
- Marcação

Com o JAMStack o HTML é exibido sem a necessidade de renderizar informações de um servidor "backend" (retaguarda), com isso, o tempo de carregamento é rápido.

Segue abaixo arquitetura "sintética" para esta jornada. Passos 1 a 11.

![](img/arquitetura_hospedagem_site.png)

### [1-3] Registro domínio

Não é obrigatório criar um domínio. No meu caso, eu registrei o domínio HTA.TEC.BR, porque faz parte do escopo do meu projeto. Para criar e registrar um domínio, primeiro você precisa cadastrar-se no site REGISTRO.BR, depois escolher o nome do domínio e em seguida, efetivar o registro, ou seja, pagar pelo registro. Mais detalhes dos processos visite o site Registro.BR: [Regras para registro de domínios .BR](https://registro.br/dominio/regras/)

![](img/registro_dominio.png)

### [4] Criar uma conta de e-mail com domínio personalizado

Novamente, não é obrigatório criar uma conta de e-mail. Criei uma conta no GMail, porque pretendemos usar o serviço de caixa postal gratuito vinculado ao domínio HTA.TEC.BR para a nossa comunicação. Mais detalhes visite: [Criar contas no GMAIL](https://support.google.com/mail/answer/56256?hl=pt-BR) e [Vincular o domínio próprio no GMAIL](https://support.google.com/a/answer/140034?hl=pt-BR).

![](img/dominio_gmail.png)

### [5-6] Preparar o GitHub

Para hospedagem dos fontes do site, é preciso criar uma conta no GitHub; [Para criar uma conta acesse](https://github.com/signup?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home).

**Resumo desta etapa:**

1. Crie uma conta de acesso GitHub;
2. Acesse o GitHub com a conta criada e crie um repositório novo, onde o site será copiado (hospedado);
3. Configure o repositório para trabalhar no formato PAGE;
4. Configure o acesso remoto via chave SSH;
5. Clone o repositório criado em sua máquina local;
6. Publique o site;

### Repositório

![](img/criar_repositorio.png)

### Repositório tipo "Pages"

![](img/repositorio_pages.png)

### Crie uma chave SSH

Para facilitar o processo de integração com o GitHub crie uma chave de acesso SSH na sua máquina e configure o GitHub para permitir a sua autenticação. Caso esteja usando **Linux** siga a dica seguinte:

Abra o shell do Linux e rode individualmente os seguintes comandos:

<!-- #region -->
```python
$ ssh-keygen # Cria um par de chaves SSH localmente.
$ eval $(ssh-agent -s) # Instância o agente SSH.
$ ssh-add ~/.ssh/acesso_site_git # Adicione a chave privada.
# Liste e copie a sua chave pública na memória e poste na configuração da SSH Key do GitHub.
$ cat ~/.ssh/acesso_site_git.pub # Chave pública
```
<!-- #endregion -->

### Configure a chave pública no GitHub

![](img/ssh_key.png)

<!-- #region -->
``` python
# Vamos testar a conexão que foi configurada.
$ ssh -T git@github.com # Teste a conexão. (Só funciona se você já tiver configurado a sua chave no Git)
# Resposta do teste de conexão:
$ Hi <seu login>! You ve successfully authenticated, but GitHub does not provide shell access.
```
<!-- #endregion -->

### Clone o repositório

Se estiver usando o Linux você pode clonar o repositório com o seguinte comando (aplique ao seu repositório, este é um exemplo): 

<!-- #region -->
``` python
$ git clone https://github.com/htaengenharia/site.git hta.github.site.local (exemplo)
```
<!-- #endregion -->

<!-- #region -->
![](img/clone_repo.png)

Depois que clonar o diretório, ajuste o aquivo "config" que está no diretório **.git** no raiz, conforme exemplo abaixo.

![](img/config.png)

### Publique o site

No exemplo abaixo criei uma página HTML com uma única imagens centralizada e postei no GitHub, usando a sequência de comandos Git abaixo:

![](img/commit.png)

Para visualizar o resultado deste "commit", acesse o seu repositório.

![](img/first_commit.png)

Para acessar o diretório via "browser" e visualizar o site precisa digitar o endereço criado e fornecido pelo GitHub, conforme ilustrado na figura 5. https://htaengenharia.github.io/site/.

### [7] Netlify Drop

O Netlify Drop é uma forma de hospedar sites e aplicativos estáticos gratuitamente. Ele automatiza o processo de hospedagem sem a necessidade de FTP ou de compilação. No nosso exemplo o Netlify permitirá a configuração de um domínio próprio apontando para o conteúdo hospedado no GitHub.
Expandindo os conceitos, este é ser um exemplo simples de CI/CD, continuous integration/continuous delivery.


**Resumo desta etapa:**

1. Cadastre-se no Netlify;
2. Importe o site do seu repositório no github;
3. Configure o deploy;
4. Primeiro deploy do site;
5. Domínio temporário.
<!-- #endregion -->

### Cadastro Netlify

Acessar o site www.netlify.com, crie uma conta e depois inicie o processo integração contínua entre o repositório com os dados do seu projeto ou site.

![](img/welcome-netlify.png)



###  Importe o site do seu repositório no github ###

![](img/home-netlify.png)


A primeira etapa nesta fase do processo de integração é vincular o seu repositório Github com o serviço Netlify. Para vincular é preciso importar um projeto da sua lista de repositórios no github. (Lembrando que o repositório precisará ser configurado para trabalhar no formato PAGE e ter arquivo index.hrml)

![](img/importar-projeto.png)


Deploy do site; após conectar no Git, selecione o repositório e configure o projeto.

![](img/deploy-part1.png)


### Configuração ###

Configuração de como ocorrerá a atualização automática do conteúdo publicado.

![](img/deploy-part2.png)



![](img/deploy-part1b.png)


### Deploy Site ###

Após configurar e aplicar ***deploy site***, o processo de víncular e configurar a integração contínua entre o conteúdo do site estático hospedado no Github e Netlify estará concluído, quando o conteúdo do site for atualizado no Github, será replicado no aplicativo Netlify que exibirá o site atualizado na Internet.

Nesta etapa um domínio temporário será criado para que você use. Não usaremos esse domínio, porque vamos trabalhar com domínio próprio.

![](img/dominio-temp.png)


O próximo passo será ajustar o DNS em Registro.BR para que seja possível usarmos o domínio próprio. Para facilitar a nossa digitação mudamos o nome do site no aplicativo Netlify (em configurações do site) para ***2ms.netlify.app***.

![](img/dominio-temp2.png)

<!-- #region -->
### [8] Registro.BR 


As próximas etapas são: 

1. Criar um sub-dominio e apontar no DNS primário para 2ms.netlify.app. Abaixo exemplo de como criar uma entrada CNAME no DNS Registro.BR. Estamos apontando um sub-domínio próprio para o domínio que o aplicativo Netlify disponibilizou.


![](img/registro_dominio-cname.png)

2. Configurar no aplicativo Netlify o sub-domínio ***jamstack.2ms.tec.br***

![](img/configurar-dns.png)

3. DNS Netlify configurado. Agora, quando digitarmos no browser ***jamstack.2ms.tec.br*** o site será exibido.

![](img/dns.png)

4. Último passo é configurar o HTTPS.

![](img/HTTPS.png)

No final da configuração, o acesso ao site poderá ocorrer também via sub-domínio ***jamstack.2ms.tec.br***
<!-- #endregion -->

<!-- #region -->
### Conclusão ###

Arquitetura JAMStack permite que tenhamos um site estático com domínio próprio sem custo de hospedagem, com atualização do conteúdo através de integração contínua (CI) usando o Github e o aplicativo Netlify Drop como principais tecnologias. Possíveis aplicações para esta solução pode ser: sites estáticos para Startups em fase de ideação, portfólios pessoais ou profissionais (CV) ou ainda trabalhos acadêmicos.


Espero ter contribuido com o seu desenvolvimento de alguma forma.



[Carlos Eugênio](https://github.com/carlosemsantana)

<!-- #endregion -->

### Referências:

[1] CI/CD - [https://www.redhat.com](https://www.redhat.com/pt-br/topics/devops/what-is-ci-cd)<br>
[2] HTML5 - [https://pt.wikipedia.org](https://pt.wikipedia.org/wiki/HTML5)<br>
[3] W3 - [https://www.w3.org/](https://www.w3.org/)<br>
[4] ReactJS - [https://pt-br.reactjs.org/](https://pt-br.reactjs.org/)<br>
[5] GitHub - [https://github.com/](https://github.com/)<br>
[6] .BR - [https://registro.br/](https://registro.br/)<br>
[7] DNS - [https://pt.wikipedia.org](https://pt.wikipedia.org/wiki/Sistema_de_Nomes_de_Dom%C3%ADnio)<br>
[8] Netlify - [https://app.netlify.com](https://app.netlify.com/drop)<br>
[9] JAMStact - [https://en.wikipedia.org](https://en.wikipedia.org/wiki/Jamstack)
