# SQL Injection


 ## 1. Lab: Este laboratório contém uma vulnerabilidade de injeção SQL no filtro da categoria do produto. Quando o usuário seleciona uma categoria, o aplicativo realiza uma consulta SQL como as seguintes: 

SELECT * FROM products WHERE category = 'Gifts' AND released = 1

Podemos perceber que o laboratório é um site de vendas de acessórios.

![image](https://user-images.githubusercontent.com/95362045/168079677-23a68b7f-af17-4c3e-83eb-8fe93bb72f15.png)

Sabemos que tem uma vulnerabilidade de SQL no filtro da categoria de produtos quando  é selecionado alguma categoria. Selecionamos a categoria lifestyle para exemplificar. E ela nos trouxe 3 produtos. 

![image](https://user-images.githubusercontent.com/95362045/168080173-00f3407a-ea22-4c02-ad1d-50bedf7d31bb.png)

Isso nada mais nada menos que é uma busca ao banco de dados e nos retorna o que solicitamos.

![image](https://user-images.githubusercontent.com/95362045/168080280-1ca00342-b790-4580-b29c-a3dfcb1ec5b7.png)

Já que queremos que os dados ocultos sejam mostrados iremos usar '+OR+1+1-- 

![image](https://user-images.githubusercontent.com/95362045/168081309-ed12d077-f4fa-4e7c-820f-7cee6502fcc7.png)

E o resultado é este: 

![image](https://user-images.githubusercontent.com/95362045/168081397-1a115fa7-9f75-4ee1-b2c7-3f86766bfac0.png)

O que fizemos foi fazer uma consulta onde devolverá todos os itens da categoria.


# SQL Injection


 ## 2. Lab: SQL injection vulnerability allowing login bypass
 
Este laboratório contém uma vulnerabilidade de injeção SQL na função de login.

Para resolver o laboratório, realize um ataque de injeção SQL que faça login no aplicativo como usuário. administrator
 
 Vamos acessar a área de login utilizando o burp. Na área de login iremos inserir no campo usuário administrador, e podemos colocar qualquer senha.

![image](https://user-images.githubusercontent.com/95362045/168106242-a1584dfc-0b73-4972-810f-8541b2e3f671.png)

Vamos clicar em log in e iremos ver a requisição. Iremos realizar uma modificação no username incluindo '-- ao final do administrator, ficando desta maneira.

![image](https://user-images.githubusercontent.com/95362045/168106635-a3b813e3-c8eb-4d6f-94ed-26a281eb8be0.png)

E iremos clicar em forward 2 vezes. Podemos perceber que conseguimos resolver a lab. 

![image](https://user-images.githubusercontent.com/95362045/168107034-3b95e53e-8707-4664-b91b-204655d26580.png)

Aqui, um invasor pode fazer login como qualquer usuário sem senha simplesmente usando a sequência de comentários do SQL para remover a verificação de senha da cláusula da consulta. Por exemplo, enviar o nome de usuário e uma senha em branco resulta na seguinte consulta: --WHEREadministrator'--

SELECT * FROM users WHERE username = 'administrator'--' AND password = ''
Esta consulta retorna o usuário cujo nome de usuário é e registra com sucesso o invasor como esse usuário. administrator



