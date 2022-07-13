# OS command injection

 ## 1. Lab: OS command injection, simple case
 
 Este laboratório contém uma vulnerabilidade de injeção de comando do SISTEMA NO verificador de estoque do produto. O aplicativo executa um comando shell contendo iDs de produtos fornecidos pelo usuário e armazena, e retorna a saída bruta do comando em sua resposta. Para resolver o laboratório, execute o comando para determinar o nome do usuário atual. whoami
 
 Vamos acessar o nosso laboratório via burp
 
 ![image](https://user-images.githubusercontent.com/95362045/168282129-efcc85a3-6947-457e-a8f2-273e679f1cc9.png)

É uma simples loja, agora iremos clicar em view details em qualquer produto de sua preferência, e ao entrar podemos nos deparar com uma opção que podemos verificar a quantidade do produto no estoque. vamos clicar em check stock com o intercept is on acionado e verificar a requisição no burp.

![image](https://user-images.githubusercontent.com/95362045/168282524-74cb9dbd-38a0-4589-b41e-27f7480f6dbf.png)

Nesta imagem podemos perceber alguns parâmetros definidos pelo sistema. Iremos mandar essa requisição para o repeater e lá iremos modificar a vigésima linha adicionando |whoami no final, ficando desta seguinte forma.

![image](https://user-images.githubusercontent.com/95362045/168282926-a15b0076-1a4b-45fd-9a55-dc2577e4326b.png)

E vamos clicar em send. E na response podemos ver que obtivemos um 200 ok e conseguimos identificar o nome do usuário atual.

![image](https://user-images.githubusercontent.com/95362045/168283003-6f92c79e-8ec5-43e1-b452-c1ba7448ddf6.png)
