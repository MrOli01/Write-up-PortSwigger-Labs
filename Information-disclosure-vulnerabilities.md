# Information disclosure vulnerabilities

## 1. Divulgação de informações em mensagens de erro

As mensagens de erro verbosas deste laboratório revelam que ele está usando uma versão vulnerável de uma estrutura de terceiros. Para resolver o laboratório, obtenha e envie o número da versão desta estrutura.

Para começar é bom termos o entendimento de o que é uma divulgação de informações. A divulgação de informações, também conhecida como vazamento de informações, é quando um site revela involuntariamente informações confidenciais aos seus usuários. Dependendo do contexto, os sites podem vazar todos os tipos de informações para um potencial invasor, incluindo:

- Dados sobre outros usuários, como nomes de usuário ou informações financeiras
- Dados comerciais ou comerciais sensíveis
- Detalhes técnicos sobre o site e sua infraestrutura

Vamos acessar o nosso laboratório e iremos analisar o site. Ele é um site normal com um catálogo de produtos, não possui nenhuma área para inserir nenhum tipo de comentário ou login para forçarmos algum erro propositalmente.

![image](https://user-images.githubusercontent.com/95362045/170295128-0f5d72e3-debc-422b-a9c6-26056f4563e9.png)

Vamos utilizar o burp para auxiliar nessa tarefa. Como burp vamos acessar qualquer produto, vamos capturar essa request.

![image](https://user-images.githubusercontent.com/95362045/170295447-09b694cc-50a6-4079-96d1-311ebd4db303.png)

Podemos notar que tem um parâmetroque carrega o id do produto, vamos mandar essa request para o repeater e iremos fazer uma modificação afim de forçar um erro que nos traga alguma informação.

Na primeira linha iremos modificar o productid para qualquer pelavra aleatória, como esta na imagem a seguir.

![image](https://user-images.githubusercontent.com/95362045/170295987-22ec0c71-08f2-4f08-a0fa-ea75ce0b6718.png)

Feito isso iremos clicar em send e ver a response. 

![image](https://user-images.githubusercontent.com/95362045/170296255-2f91f2a2-10a7-4550-b4d4-9de9ae6681b3.png)

Podemos reparar que o laboratório está usando apache struts  2 2.3.31. Agora é só copiar a versão e finalizar a challenge.

![image](https://user-images.githubusercontent.com/95362045/170296540-ef9004f6-c1d7-49e4-9ece-1d0684d3833f.png)

## 2.  Information disclosure on debug page

Este laboratório contém uma página de depuração que divulga informações confidenciais sobre o aplicativo. Para resolver o laboratório, obter e submeter a variável ambiental. SECRET_KEY

Vamos acessar o laboratório. pelas informações tem uma laboratório que contém uma páina de depuração que divulga as informações sobre o aplicativo. 
Ao acessar o laboratório vamos ir em inspecionar.

![image](https://user-images.githubusercontent.com/95362045/170320675-3c91028a-36c2-49b7-84b3-1ab64fab3131.png)

Podemos observar que tem umk link que leva ao phoinfo.php. Então vamos copiar o caminho e inserir na url do laboratório /cgi-bin/phpinfo.php

![image](https://user-images.githubusercontent.com/95362045/170320936-9a985f79-8b59-4683-bd9f-0b4d6c1e45ec.png)

Ao acessar podemos ver que temos algumas informações do PHP e suas configurações. Nesse instante podemos dar Ctrl F e pesquisar sobre SECRET_KEY 

![image](https://user-images.githubusercontent.com/95362045/170321383-cb302ffc-86ed-4ac0-8250-3bb2fc84278c.png)

Bingo, conseguimos a secret key e agora é só finalizar a lab.

![image](https://user-images.githubusercontent.com/95362045/170321580-89c0be11-ea32-4b7b-b801-f8860b8c9b15.png)

## 3. Source code disclosure via backup files

Este laboratório vaza seu código fonte através de arquivos de backup em um diretório oculto. Para resolver o laboratório, identifique e envie a senha do banco de dados, que é codificada no código fonte vazado.

Bom já sabemos que tem um diretório oculto que precisamos descobrir, geralmente o diretório robots.txt mostra quais diretórios estão ocultos para serviços de pesquisas. Emtão iremos testar esse laboratório incluindo ao final do URL /robots.txt 

![image](https://user-images.githubusercontent.com/95362045/170325013-7af81fcc-d408-4e05-9ba8-39fcfd5068ab.png)

Aqui percebemos que tem um diretório oculto /backup, então colhendo essa informação vamos tentar o acesso.

![image](https://user-images.githubusercontent.com/95362045/170325815-52c601c0-2c36-4727-a406-18f0b69bb406.png)

![image](https://user-images.githubusercontent.com/95362045/170326376-c016c5b2-e2d4-415f-a72b-4644ab6d7edb.png)

Agora acessando podemos ver um código fonte em java, e nele se encontra uma  senha codificada para um banco de dados postgres. 

![image](https://user-images.githubusercontent.com/95362045/170326261-333e5263-7e62-4655-a62c-1cba38810487.png)

Analisando podemos encontrar a senha codificada, agora é só cipar e finalizar a lab

## 4. Authentication bypass via information disclosure

A interface de administração deste laboratório tem uma vulnerabilidade de desvio de autenticação, mas é impraticável explorar sem o conhecimento de um cabeçalho HTTP personalizado usado pela front-end.

Para resolver o laboratório, obtenha o nome do cabeçalho e use-o para contornar a autenticação do laboratório. Acesse a interface administrativa e exclua a conta de Carlos. Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Vamos acessar o laboratório e se logar, e posteriormente vamos tentar entrar na área administrativa usando o caminho de diretorio /admin

![image](https://user-images.githubusercontent.com/95362045/170357679-b638598a-043a-426f-8d7e-2182af57e2a3.png)

Na imagem diz que a Interface administrativa é disponível apenas para usuários locais.

Agora vamos até o burp analisar a resquest GET /admin

![image](https://user-images.githubusercontent.com/95362045/170357985-5ff966a1-4211-4db3-bea5-9168b5a2606a.png)

Agora vamos enviar para o repeater e fazer uma alteração. Ao invés de GET vamos alterar para TRACE /admin e iremos clicar em send.

![image](https://user-images.githubusercontent.com/95362045/170358299-5b7c99ee-2bcd-45d9-b777-9cc6dd3f46a9.png)

O método HTTP TRACE realiza um teste de loopback enviando uma mensagem por todo o caminho até o recurso alvo no qual foi destinado, provendo um mecanismo útil para debug. 

![image](https://user-images.githubusercontent.com/95362045/170359172-62f68463-ea3f-4553-89e6-d05f09dea91e.png)

Podemos ver que não está pegando o local host obviamente, e vamos alterar para o IP 127.0.0.1

Agora iremos em proxy e Options, vamos navegar até seção "Correspondência e Substituição" e clique em "Adicionar". Deixe a condição da partida em branco, mas no campo "Substituir", entre:

X-Custom-IP-Authorization: 127.0.0.1

O  Proxy adicionará este cabeçalho a cada solicitação enviada.

Agora é só navegar até o laboratório e atualizar que poderemos remover o usuário carlos.
