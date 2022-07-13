# HTTP Host header attacks

## 1. Lab: Basic password reset poisoning

Este laboratório é vulnerável a envenenamento por redefinição de senha. O usuário clicará descuidadamente em quaisquer links em e-mails que receber. Para resolver o laboratório, faça login na conta do Carlos. carlos

Você pode fazer login em sua própria conta usando as seguintes credenciais: . Todos os e-mails enviados para esta conta podem ser lidos através do cliente de e-mail no servidor de exploração. wiener:peter

Vamos até a página de login e observar a funcionabilidade "Esqueci sua senha?" Vamos solicitar uma redefinição de senha para a propria conta.

![image](https://user-images.githubusercontent.com/95362045/172205163-0e38ea51-6402-4c9f-b6af-925000a25dc9.png)

Vamos entrar no nosso email em exploit server e verificar que recebemos um link para troca de senha, vamos clicar e colocar a senha de nossa preferência.

![image](https://user-images.githubusercontent.com/95362045/172205404-e6c8e8b3-e1f0-4a17-8ea3-06ac4a60bd97.png)

Vamos agora no burp em HTTP history, vamos observar que a solicitação é usada para acionar o e-mail de redefinição de senha. Contém o nome de usuário cuja a senha está sendo redefinida como parâmetro. Vamos enviar o pedido para o repeater

![image](https://user-images.githubusercontent.com/95362045/172229860-f8901c32-c30b-4f7c-bd01-108d5071916f.png)

No Burp Repeater, observe que podemos alterar o cabeçalho Host para um valor arbitrário e ainda acionar com sucesso uma redefinição de senha. Vamos voltar para o servidor de e-mail e ver o novo e-mail que recebemos. Observe que a URL no e-mail contém seu cabeçalho host arbitrário em vez do nome de domínio usual. Vamos voltar no repeater e vamos alterar o cabeçalho host para um valor aleatório e ainda vamos acionar com sucesso uma redefinção de senha.

![image](https://user-images.githubusercontent.com/95362045/172230533-5fff5065-156d-4d92-a624-24118c0bc4e6.png)

Iremos volrar para o servidor de email e verificar o novo email que recebemos. Observemos que a URL do email contém um host arbitrário em vez do dominio usual.

![image](https://user-images.githubusercontent.com/95362045/172230724-a0e9a313-85fa-4c4d-b4a8-8f2caeda7ddf.png)

Vamos voltar para o repeater e vamos alterar o cabeçalho host para o nome de dominio do servidor de exploração e alteraremos o parametro de usuário para carlos

![image](https://user-images.githubusercontent.com/95362045/172232305-92774364-0cdb-43d9-80fe-481d18423c94.png)

Vamos para o servidor de exploração e abriremos o registro de acesso. Veremos uma solicitação com o parâmetro contendo o token de redefinição de senha de Carlos. Anotaremos esse token

![image](https://user-images.githubusercontent.com/95362045/172236104-0356ceae-6748-40f6-b2af-16bfd8e90e31.png)

Vamos até o nosso email e pegar o link de redefinição de senha. Vamos copiar o link e apenas alterar o token pelo que pegamos.

![image](https://user-images.githubusercontent.com/95362045/172236323-8f9d566a-bd23-4012-911c-83bd28a1784e.png)

Alteremos a senha para qualquer senha aleatória. e clica em submit 

![image](https://user-images.githubusercontent.com/95362045/172236560-6e16dc2c-7d3f-4ac0-8958-f5777dcd745a.png)

Agora é só logar na conta do carlos.

![image](https://user-images.githubusercontent.com/95362045/172236730-a2f494db-5c92-459b-9f04-a4c3b09d425f.png)

laboratório resolvido.

![image](https://user-images.githubusercontent.com/95362045/172236794-0b86b205-0345-4714-94d0-fb77d14c70b1.png)

## 2. Lab: Host header authentication bypass

Este laboratório faz uma suposição sobre o nível de privilégio do usuário com base no cabeçalho http host.

Para resolver o laboratório, acesse o painel de administração e exclua a conta de Carlos.

Vamos acessar o nosso laboratório, e percebemos que recebemos um status code 200, da mesma forma podemos fazer uma alteração do host. Vamos tentar acessar o robots.txt 

![image](https://user-images.githubusercontent.com/95362045/172239652-8f623ba4-d010-4d70-ada1-ec05ce1e020e.png)

Podemos perceber que tem um /admin desabilitado para buscas de ferramentas de pesquisa. Vamos tentar acessar o /admin Aqui está dizendo que apenas usuários locais tem permissão de acesso ao painel administrativo.

![image](https://user-images.githubusercontent.com/95362045/172239749-cd702214-a00c-4923-a224-1c8aba4715ae.png)

Vamos ir até a request /admin e alterar o parâmetro host: localhost e clicar em send.

![image](https://user-images.githubusercontent.com/95362045/172239963-eb5bdc7d-8e88-405a-96e3-fd6f2adb153e.png)

Podemos perceber qwe já temos permissões de administrador.

![image](https://user-images.githubusercontent.com/95362045/172240074-d3e6fced-d160-4448-9021-c62d8208274d.png)

Agora olhando a response podemos perceber qual é o caminho para deletar o usuário carlos.

![image](https://user-images.githubusercontent.com/95362045/172240183-5d41759b-6eb7-4787-bb72-a7f3c3924986.png)

Agora iremos alterar a linha de solicitação ficando desta forma.

![image](https://user-images.githubusercontent.com/95362045/172240494-f860eebb-d5c4-4c1d-9c95-15b97250be2f.png)

E finalizamos a lab

![image](https://user-images.githubusercontent.com/95362045/172240569-33bfc953-6563-43ba-85a8-38e8ef2856ad.png)




