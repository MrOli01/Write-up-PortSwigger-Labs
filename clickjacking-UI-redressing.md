# Clickjacking (UI redressing)

## Lab: Basic clickjacking with CSRF token protection

Este laboratório contém funcionalidade de login e um botão de conta de exclusão protegido por um token CSRF. Um usuário clicará em elementos que exibem a palavra "clique" em um site de isca. Para resolver o laboratório, crie alguns HTML que emoldura a página da conta e engane o usuário a excluir sua conta. O laboratório é resolvido quando a conta é excluída. Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter.

Para começar iremos realizar nosso login.

![image](https://user-images.githubusercontent.com/95362045/168834442-987d4bcf-37a4-427e-9dae-5a4878b990d7.png)

Posteriormente teremos que criar um HTML e incluir no servidor de exploração do laboratório. o bloco de notas.

![image](https://user-images.githubusercontent.com/95362045/168836085-c8ef628a-e3ac-46d1-92a4-07b48cb8946b.png)

Aqui definimos um estilo que é definido por style e definimos alguns parâmetros. Agora iremos realizar algumas modificações no modelo. Vamos substituir o atributo iframe com a URLda pagina da conta de usuário do site de destino. 

![image](https://user-images.githubusercontent.com/95362045/168837535-dd1d6b85-b8dc-41b4-a3af-d541d9bc3405.png)

Após definirmos a URL iremos modificar o nosso style para ele ficar padronizado, ficando desta forma.

![image](https://user-images.githubusercontent.com/95362045/168838104-73898ee5-ce5c-4311-ab9a-930ed73a1945.png)

Se copiarmos esse código e colocarmos em go to exploit e ver como ele responde iremos ver que o estilo fica desta forma.

![image](https://user-images.githubusercontent.com/95362045/168838294-14bde017-c4f5-4dee-97cb-739dd295d0da.png)

Agora iremos fazer outras modificações, iremos acrescentar um botão escrito click aqui para induzir a vítima, ficando desta forma.

![image](https://user-images.githubusercontent.com/95362045/168839527-0f5c2901-414f-426f-85f9-cfbd5f7ff8a4.png)

Agora se formos analisar no view exploit podemos perceber que o click me está posicionado no lugar indesejado então vamos fazendo alterações no style para ele ficar sobreposto no botão delete account. Definimos o parmêmetro top em 515 e o left em 60 ficando desta forma:

![image](https://user-images.githubusercontent.com/95362045/168840336-8bb653e9-81af-44ca-8ae5-d0a66e8a7ff2.png)

![image](https://user-images.githubusercontent.com/95362045/168840397-2e09b54c-151c-4ac2-8bd7-4d86953abc0a.png)

Agora podemos diminuit a opacidade do site para que fique totalmente desapercebido o real site que está por trás. podemos definir em opacity: 0.000001; Ficando desta forma.

![image](https://user-images.githubusercontent.com/95362045/168840883-ae2e91cc-9460-496e-9ed8-362eb2e82ccd.png) 

Agora é só clicar em diliver exploit to victim e concluir a lab.

![image](https://user-images.githubusercontent.com/95362045/168841148-f081cc22-8eea-4a1b-bb37-e6f0251cacc8.png)

Muita das vezes o style é mais modificado, a aparência fica melhor, mas como é afim de realizar uma simples lab não foi preciso aperfeiçoar muito.

## Lab: Clickjacking with form input data prefilled from a URL parameter

Este laboratório estende o exemplo básico de clickjacking em Lab: Clickjacking básico com proteção de token CSRF. O objetivo do laboratório é alterar o endereço de e-mail do usuário, prepopulando um formulário usando um parâmetro de URL e seduzindo o usuário a clicar inadvertidamente em um botão "Atualizar e-mail". Para resolver o laboratório, crie alguns HTML que emoldura a página da conta e engane o usuário a atualizar seu endereço de e-mail clicando em uma isca "Clique em mim". O laboratório é resolvido quando o endereço de e-mail é alterado. Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Iremos entrar no laboratório e acessar a nossa conta wiener:peter

![image](https://user-images.githubusercontent.com/95362045/169073690-f47aa38a-1a29-4f45-b458-7612b3e728f2.png)

Como foi dito anteriormente teremos que fazer um modelo HTML comparado com o do outro laboratório. Para facilitar vamos acessar o go to exploit server, e vamos descer até o campo body e realizar nosso script.

![image](https://user-images.githubusercontent.com/95362045/169074306-2c5d109f-05af-4471-8510-2c0b7af5b741.png)

![image](https://user-images.githubusercontent.com/95362045/169074419-0a668b86-2894-46d7-9c16-1d0a3b2969f1.png)

![image](https://user-images.githubusercontent.com/95362045/169075439-313275f0-e6a6-4b82-97c8-d89539425636.png)

Realizamos toda a escrita da estrutura do nosso script, agora precisamos definir os valores para cada uma. Vamos fazer os seguintes ajustes.

- Substituir $url pela URL da pagina da conta do usuário do site de destino que contém o formulário "Atualizar e-mail"
- Substituir os valores de pixel adequados para as variáveis $height_value e $width_value do iframe (vamos tentat 700px e 500px, respectivamente).
- Substituir os valores adequados dos pixels para as variáveis $top_value e $side_value do conteúdo da web isca para que o botão "Atualizar e-mail" e o "Teste-me" ação de isca alinhada (vamos tentar 400px e 80px, respectivamente).
- Definir o valor de opacidade $opacity para garantir que o iframe de destino seja transparente. Inicialmente vamos usar  uma opacidade de 0.1 para que você possa alinhar as ações do iframe e ajustar os valores de posição conforme necessário. Para que de certo teremos que usar um valor de 0,0001.

Feito todas essas alterações iremos clicar em store e posteriormente vamos ver como ficou clicando em view Exploit.

![image](https://user-images.githubusercontent.com/95362045/169082576-7023576f-6cf1-4cc7-a198-7ae7a6cc4753.png)

Conseguimos alinhar o nosso click me sobre o botão de redefinir o email. Agora é só clicar em deliver exploit to victim e concluir a lab.

## Lab: Clickjacking with a frame buster script

Este laboratório é protegido por um buster de quadro que impede que o site seja emoldurado. Você pode contornar o buster de quadros e realizar um ataque de clickjacking que altera o endereço de e-mail dos usuários? Para resolver o laboratório, crie alguns HTML que emoldura a página da conta e engane o usuário a alterar seu endereço de e-mail clicando em "Clique em mim". O laboratório é resolvido quando o endereço de e-mail é alterado. Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Esse exercício lembra o anterior, porém agora temos uma barreira que é o buster de quadro, que impede que o site seja emoldurado. Como feito anteriormente iremos acessar a nossa conta.

![image](https://user-images.githubusercontent.com/95362045/169084467-d3b0ef37-95ea-4fe9-b296-b830063b3be1.png)

Como feito anteriormente iremos pegar o nosso script html porém agora teremos leves mudanças afim de burlar a proteção. A seta pode nos mostrar que adicionamos a tag iframe sandbox="allow-forms", neste laboratório usando essa tag podemos neutralizar o script buster pois o iframe não pode perificar se é ou não janela superior.

![image](https://user-images.githubusercontent.com/95362045/169084654-fc3ac0dc-8ddc-42d9-9efd-2f2a7d69bcb9.png)

- Faça os seguintes ajustes no modelo:
- Substituir no atributo iframe com a URL da página da conta de usuário do site de destino, que contém o formulário "Atualizar e-mail". $urlsrc
- Substituir os valores de pixel adequados para as variáveis $height_value e $width_value do iframe  700px e 500px, respectivamente.
- Substitua os valores adequados dos pixels para as variáveis $top_value e $side_value do conteúdo da web isca para que o botão "Atualizar e-mail" e o alinhamento de ação de isca "Test me"  385px e 80px, respectivamente.
- Definir o valor de opacidade $opacity para garantir que o iframe de destino seja transparente.Vamos uma opacidade de 0.1 para que você possa alinhar as ações do iframe e ajustar os valores de posição conforme necessário.
Observe o uso do atributo que neutraliza o script buster de quadro. sandbox="allow-forms"

Feito essas alterações vamos clicar em store e posteriormente View exploit.

![image](https://user-images.githubusercontent.com/95362045/169086251-9cc298b8-48f9-4759-aa41-2f9c830758c1.png)

Podemos perceber que teremos que alterar os valores citados anteriormente afim de sobrepor o click me com o botão de Update Email ao fundo. 

![image](https://user-images.githubusercontent.com/95362045/169087763-7cb4e0a6-5990-4679-989a-d159fd147169.png)

Definimos um top: 445px e alinhamos. Agora é só clicar em deliver exploit to victim e finalizar a lab


