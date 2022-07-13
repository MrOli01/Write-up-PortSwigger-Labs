# Server-side request forgery (SSRF)

## 1. Lab: Basic SSRF against the local server

Este laboratório tem um recurso de verificação de estoque que busca dados de um sistema interno.

Para resolver o laboratório, altere a URL de verificação de estoque para acessar a interface administrativa e excluir o usuário . http://localhost/admincarlos

Iremos ter o entendimento de como funciona o site, para conseguirmos deletar o usuário precisamos ter acesso admin no laboratório. Nesta imagem podemos perceber que ao acessar com o diretório /admin não temos acesso. Então vamos clicar em algum produto e com o intercept on vamos checar o estoque do produto.

![image](https://user-images.githubusercontent.com/95362045/170536535-3f5f11c5-4eb6-455e-a66e-962b228e660a.png)

Nesta imagem podemos ver que o laboratório consulta uma API para pesquisar a quantidade de produto que tem no estoque.

![image](https://user-images.githubusercontent.com/95362045/170536917-c6a03cd3-f7d2-4d41-84fb-7bb02fc11cf5.png)

Então iremos modificar essa URL definindo uma pesquisa no localhost como descrito no laboratório. Vamos encaminhar para o repeater e modificaremos o caminho. Ficando desta forma: 

![image](https://user-images.githubusercontent.com/95362045/170538052-ddd3c5f5-7754-4e62-962c-460c1d049f54.png)

Na response podemos ver todo o HTML e nele à um caminho para deletar o usuário, se encontra aqui:

![image](https://user-images.githubusercontent.com/95362045/170538289-b98e4181-f325-48fa-b697-1ddc1594e0b0.png)

Porém como queremos deletar o usuário carlos iremos modificar apenas o nome e colocar em nova URL do laboratório. 

![image](https://user-images.githubusercontent.com/95362045/170538541-60da1b74-ee18-4f10-aabd-603890c97038.png)

E finalizamos o laboratório.

## 2. Basic SSRF against another back-end system

Este laboratório tem um recurso de verificação de estoque que busca dados de um sistema interno.

Para resolver o laboratório, use a funcionalidade de verificação de estoque para digitalizar o intervalo interno para uma interface de administração na porta 8080 e, em seguida, use-o para excluir o usuário . 192.168.0.Xcarlos

Vamos acessar o nosso laboratório como feito anteriormente, vamos acessar algum produto e com intercept on iremos verificar o estoque de algum produto, e iremos analisar a sua request.

![image](https://user-images.githubusercontent.com/95362045/170565821-f89fc5a4-3920-4922-9704-c1f5653a48e4.png)

Então como está no anunciado teremos que verificar o ultimo digito do Ip como descrito no enunciado 192.168.0.x. Primeiramente vamos fazer uma modificação em stockApi ficando desta maneira.

![image](https://user-images.githubusercontent.com/95362045/170566191-c1d3a206-4bcd-437b-b485-7d2f1f1fe50b.png)

Após ter feito essa modificação daremos um Ctrl + i para enviar essa request para o intruder, iremos fazer um ataque de força bruta com numeros afim de descobrir o ultimo digito do IP. Antes de tudo, na área de Payload Positions iremos dar um clear $ e faremos uma marcção em Add na área demarcada na imagem a seguir.

![image](https://user-images.githubusercontent.com/95362045/170566818-b047ea4c-414f-416c-82f5-b54c9282f37e.png)

Dessa maneira vamos definir o Payload type como numbers, definir também os paramêtros from, to, step. Na imagem diz que iremos fazer um ataque do numero 1 ao 255 e depois clicar em Start Attack.

![image](https://user-images.githubusercontent.com/95362045/170566586-c2eee802-25ac-4711-9705-8b9089a8f138.png)

Aqui começa as tentativas, podemos ver vários status code, mas o que nos interessa é o 200, podemos ver que o numero 48 foi.

![image](https://user-images.githubusercontent.com/95362045/170571110-6e69424d-0ff6-4fa1-9774-f40fad72cdb5.png)

Feito isso vamos até o burp novamente e pegar a request ao conferir se tem estoque

![image](https://user-images.githubusercontent.com/95362045/170572059-3e3d21ec-31ce-4b01-a445-1f1b06e49ffa.png)

![image](https://user-images.githubusercontent.com/95362045/170572878-7a3d2fab-ec21-4e1c-996a-c2b05deec682.png)

![image](https://user-images.githubusercontent.com/95362045/170573020-a910d7ba-2637-4e84-9f73-1bfcfc26c274.png)


