# Authentication bypass via OAuth

 ## 1. Authentication bypass via OAuth implicit flow
 
 Este laboratório usa um serviço OAuth para permitir que os usuários façam login com sua conta de mídia social. A validação falha pelo aplicativo do cliente permite que um invasor faça login nas contas de outros usuários sem saber sua senha. Para resolver o laboratório, faça login na conta do Carlos. Seu endereço de e-mail é . carlos@carlos-montoya.net. Você pode fazer login com sua própria conta de mídia social usando as seguintes credenciais: . wiener:peter

Primeiramente acessando o laboratório em my account teremos que logar com a nossa midia social que é wiener:peter

![image](https://user-images.githubusercontent.com/95362045/168126363-fc9526f7-6925-40c7-8c98-fd8ccd407bd5.png)

E posteriormente é só clicar em continue. Agora que foi autorizado a entrar em sua conta vamos ver as requestse em HTTP history. Vamos ver a requisição GET /auth?client_id= que compoe o fluxo do OAuth.

![image](https://user-images.githubusercontent.com/95362045/168126991-55c79e4c-a384-4359-b110-63e1d3211e74.png)

Observe que o aplicativo do cliente (o site do blog) recebe algumas informações básicas sobre o usuário do serviço OAuth. Em seguida, registra o usuário enviando uma solicitação contendo essas informações para seu próprio ponto final, juntamente com o token de acesso. POST/authenticate

![image](https://user-images.githubusercontent.com/95362045/168127234-5c67a512-a04c-4500-8802-e8af52bd64d6.png)

Agora iremos mandar para o repeater e vamos modificar o email para carlos@carlos-montoya.net

![image](https://user-images.githubusercontent.com/95362045/168127652-0bd4c42d-ab28-4863-bf8b-1e150c01a5e7.png)

Vamos clicar com o botão direito do mouse na request e vamos enviar ela para request in browser e vamos em in original session e clica em copy. Abrindo um novo navegador iremos colar a URL copiada e teremos acesso a conta do carlos sem mesmo ter acesso a senha.

![image](https://user-images.githubusercontent.com/95362045/168128109-0fa561c7-bbe7-4d50-a1af-0a26bbe179ab.png)
![image](https://user-images.githubusercontent.com/95362045/168128129-f21401f0-2a25-4a9f-a412-42a57015bbaa.png)
