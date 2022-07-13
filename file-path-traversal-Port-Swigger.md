# Directory Traversal

 ## 1. File Path Traversal, Traverse Sequences Locked with Absolute Path Offset 

Este laboratório contém uma vulnerabilidade transversal de caminho de arquivo na exibição de imagens do produto.
O aplicativo bloqueia sequências transversais, mas trata o nome do arquivo fornecido como sendo relativo a um diretório de trabalho padrão. Para resolvermos o laboratório, teremos que recuperar o  conteúdo do arquivo. **/etc/passwd**

### Vamos acessar o nosso laboratório.

Vamos então acessar o código fonte para resolver o caminho do arquivo do laboratório, o intuito é recuperar os arquivos que estão no /etc/passwd.
Para esse exercicio iremos usar o BurSuite para interceptarmos as requisições. Então podemos acessar o laboratório de duas maneiras, entrando via Chromium que é o navegador prório do Burp ou configurando o navegador de sua preferência, para maior agilidade utilizaremos a primeira opção.

Primeiramente iremos dar um intercept off para não realizar a primeira requisição ao acessar.

![image](https://user-images.githubusercontent.com/95362045/167206531-89379a83-0ddd-4a9d-8697-8e09800e29b1.png)

Sendo assim abrindo o browser iremos navegar pelo codigo fonte da página teclando F12.

![image](https://user-images.githubusercontent.com/95362045/167206904-73a66113-e239-46ca-b418-989607700bdd.png)

Como pode ser visto iremos navegar pelo codigo fonte até section class="container-list-titles">.

![image](https://user-images.githubusercontent.com/95362045/167207173-ea332740-d723-4395-8152-3a1dde657862.png)

Neste momento vamos acessar o primeiro link da tag <img src=> Ao abrir podemos ver uma imagem e na URL podemos ver uma busca da imagem como por exemplo o filename=1.jpg. Agora poderemos interceptar e dar um F5 na página para o burp pegar a requisição

![image](https://user-images.githubusercontent.com/95362045/167208732-c77069a1-508c-457c-bec4-a672d3452909.png)

Agora podemos ver alguns parâmetros das requisições no Burp.

![image](https://user-images.githubusercontent.com/95362045/167208913-357a42bb-0ed1-4fc6-8502-bb5cd19e216d.png)

Agora iremos encaminhar para o repeter para manipularmos essa requisição, podemos usar um atalho teclando Ctrl + R.

![image](https://user-images.githubusercontent.com/95362045/167209167-cf1ef5a4-1226-4f61-a224-c897b133565c.png)

A esquerda podemos ver a request e a direita a response que será a resposta dessa requisição à esquerda.

![image](https://user-images.githubusercontent.com/95362045/167209994-4e1ac341-5770-49ce-ad64-93a5154db6f8.png)
![image](https://user-images.githubusercontent.com/95362045/167210963-fd6851fa-126e-4058-ad29-d50df94404dc.png)

Bingo, podemos ver que recebemos um 200 Ok, é um status code que a requisição foi aceita, e podemos ver o conteúdo abaixo com todo os detalhes. Agora para validarmos podemos acessar o site da mesma maneira do burp por fora do burp para validar no sistema da PortSwigger.

![image](https://user-images.githubusercontent.com/95362045/167211278-794002a3-d44d-4104-b810-2b5f9bf60aa8.png)
![image](https://user-images.githubusercontent.com/95362045/167211440-139abddc-3f87-4051-8daa-1156ee815883.png)

# Directory Traversal

 ## 2. File path traversal, simple case
 
Este laboratório contém uma vulnerabilidade transversal de caminho de arquivo na exibição de imagens do produto. Para resolvermos o laboratório, teremos que recuperar o conteúdo do arquivo. /etc/passwd, Iremos acessar o laboratório pelo chromium. Ao entrar iremos interceptar as requisições e clicar em qualquer produto em View Details.

Essa é a resposta da nosso requisição:

![image](https://user-images.githubusercontent.com/95362045/167430841-9f0dc92d-0057-4f1e-9fc6-ea2f15ca3717.png)

Iremos clicar em forward para dar direcionamento na requisição:

![image](https://user-images.githubusercontent.com/95362045/167431499-cc93583a-aaad-4524-bc69-4f4cf39c068f.png)

Agora temos novos parametros. iremos realizar uma alteração na primeira linha ficando: GET /image?filename=../../../etc/passwd HTTP/1.1 e daremos um novo forward.
Iremos acessar a aba HTTP history e selecionando a seguinte URL:

![image](https://user-images.githubusercontent.com/95362045/167432199-0a22e497-bd4b-4d1b-bde4-bb1df5ae407c.png)

Podemos ver na imagem seguinte que temos como ver a Original Request e a Edited Request, e ao lado direito a response da request editada que nos trás o conteúdo do arquivo /etc/passwd
![image](https://user-images.githubusercontent.com/95362045/167432822-eb5d41a3-4960-4841-9373-053b9f3a382b.png)

# Directory Traversal

 ## 3. File path traversal, traversal sequences stripped non-recursively
 
 Este laboratório contém uma vulnerabilidade transversal de caminho de arquivo na exibição de imagens do produto. O aplicativo tira sequências de travessia de caminho do nome de arquivo fornecido pelo usuário antes de usá-lo. Para resolver o laboratório, teremos que recuperar o conteúdo do arquivo. /etc/passwd
 
 Iremos realizar os mesmos passos das atividades anteriores realizando a captura das requisições pelo burp. Acessando o site e antes de clicar em qalquer View Details iremos ligar a interceptação. Daremos proceguimento clicando em forward 1 vez. 
 
 ![image](https://user-images.githubusercontent.com/95362045/167449682-a9a9b42a-e676-4570-b4db-2b90a742be4e.png)
 
 Quando chegarmos nesta parte como mostrado na imagem a cima iremos fazer uma modificação no metodo GET, substituindo o 58.jpg por ....//....//....//etc/passwd
 Diferentemente do outro esse laboratório tira sequências transversais de caminhos de arquivos como uma tática defensiva, então usaremos sequências aninhadas para contornar essa desefa, ficando neste jeito

![image](https://user-images.githubusercontent.com/95362045/167451124-c405d213-c739-4a24-998f-3368fe7e9d08.png)

Posteriormente iremos dar um forward e vamos na aba HTTP History e acharmos na coluna URL /image?filename=58.jpg. 

![image](https://user-images.githubusercontent.com/95362045/167451333-4fdf586b-df26-4917-8a4a-3bc8b128c004.png)

Podemos ver que temos detalhadamento os dados que se encontra em /etc/passwd

# Directory Traversal

 ## 4.  File path traversal, traversal sequences stripped with superfluous URL-decode 
 
 Este laboratório contém uma vulnerabilidade transversal de caminho de arquivo na exibição de imagens do produto. A entrada de blocos de aplicação contendo sequências transversais de caminho. Em seguida, executa um URL-decodificador da entrada antes de usá-la. Para resolver o laboratório, rteremos que recuperar o conteúdo do arquivo. /etc/passwd
 
 Iremos acessar o Bupr e usar o chromium. Iremos utilizar as mesmas métricas dos exercicíos anteriores. Iremos dar um forward até chegarmos nessas requisições. Na primeira linha apó-s o sinal de "=" iremos realizar uma alteração. Colocaremos da seguinte forma: %252f..%252f..%252fetc/passwd 

![image](https://user-images.githubusercontent.com/95362045/167638395-b149aae0-4f27-4f68-9f3a-9fa3040e9e89.png)

Podemos perceber que conseguimos ter acesso a /etc/passwd. Para entendermos vamos ter que olhar primeiro a tabela decode URL para saber como funciona. A URL ela codifica caractéres especiais pois muitos deles possuem uma função especifica na URL como definir ou separar parâmetros por exemplo, então para a URL diferenciar isso se usa  como essa tabela 

![image](https://user-images.githubusercontent.com/95362045/167640159-2c000f68-2e3c-4725-aa76-0664d623cd72.png)
