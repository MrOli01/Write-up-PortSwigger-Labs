 # Acess Control Vulnerabilities 


 ## 1. Lab: Unprotected admin functionality
 
Este laboratório tem um painel de administração desprotegido. Resolva o laboratório excluindo o usuário . carlos

Vamos acessar o nosso laboratório. Já vimos que os sites normalmente possuem um diretório chamado robots.txt. O Protocolo de Exclusão de Robôs é um método empregado pelos administradores de sistemas para informar aos robots visitantes quais diretórios de um site não devem ser vasculhados por eles.

Sabendo vamos colocar /robots.txt no final da nossa URL e daremos enter.

![image](https://user-images.githubusercontent.com/95362045/168632063-138990d9-a253-410f-9da0-d7b0621f85bb.png)

Já temos uma informação que é a que precisamos que é o painel administrativo, então vamos apagar o /robots.txt e colocaremos desta maneira /administrator-panel

![image](https://user-images.githubusercontent.com/95362045/168632383-9e7eea82-2a83-454a-aa1b-02d56ceada5f.png)

Conseguimos ter acesso aos usuários e temos o poder de excluir qualquer um, esse é um perigo de ter o painel administrativo sem ter nenhum metodo de autenticação ou autorização. Agora iremos deletar o usuário carlos e finalizar a nossa lab

![image](https://user-images.githubusercontent.com/95362045/168632636-7e1a1697-aa65-4c32-967a-72bc482f3653.png)


## 2. Lab: Unprotected admin functionality with unpredictable URL

Este laboratório tem um painel de administração desprotegido. Está localizado em um local imprevisível, mas o local é divulgado em algum lugar no aplicativo.
Resolva o laboratório acessando o painel de administração e usando-o para excluir o usuário . carlos

Vamos acessar o nosso laboratório, sabemos que tem um painel administrativo de forma desprotegida em um local imprevisível mas está em algum lugar do aplicativo.
Vamos abrir o código fonte da página e analisar. 

![image](https://user-images.githubusercontent.com/95362045/168634531-175451e2-4c11-404a-b4fa-4ea981094493.png)

Logo de cara vemos um javascript que informa a localidade do painel admministrativo. /admin-dkaxmj

![image](https://user-images.githubusercontent.com/95362045/168634882-14a79c30-df63-4763-b8f9-215068d5158d.png)

Novamente como o outro exercício vamos deletar o usuário carlos.

![image](https://user-images.githubusercontent.com/95362045/168634996-bc73a5ad-ce6c-4392-8d82-d8786a416e94.png)

## 3. Lab: User role controlled by request parameter

Este laboratório tem um painel de administração em , que identifica administradores usando um cookie forjado. /admin. Resolva o laboratório acessando o painel de administração e usando-o para excluir o usuário . carlos. Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Vamos acessar o burp iremos logar na nossa conta wiener:peter. Vamos pegar a requisição do login

![image](https://user-images.githubusercontent.com/95362045/168637535-71a32c22-cc6f-443d-9572-ede4f2704e35.png)

Vamos primeiramente analisar quando tentamos acessar a área administrativa com o nosso usuário sem permissões.

![image](https://user-images.githubusercontent.com/95362045/168637816-43c92477-0574-4b8d-bcaa-88a8bd9dfece.png)

Diz que somente usuários como administrador pode ter acesso. Então iremos voltar para o burp e ir na aba repeater e dar um send na requisição, podemos ver a resposta 

![image](https://user-images.githubusercontent.com/95362045/168638034-a1424f78-4bd8-45bc-8b79-7e69e3bbc847.png)

Voltando para a requisição fora do repeater no set-cookies podemos notar que diz que Admin=false, quer dizer que não tenho permissões administrativas, então iremos modificar para true, dizendo que tenho permissões.

![image](https://user-images.githubusercontent.com/95362045/168650513-502fd678-ee64-4c61-9366-276324e9b163.png)

Então clicaremos em forward e indo ao navegador podemos observar o painel de adm

![image](https://user-images.githubusercontent.com/95362045/168651760-7017e9c1-b0d2-4bc3-be46-05c2476c6ec0.png)

![image](https://user-images.githubusercontent.com/95362045/168652273-b333c035-6bed-4752-ac32-bd12e56d3859.png)

Agora é só deletar o usuário e finalizar a lab.


## 4. Lab: User role can be modified in user profile

Este laboratório tem um painel de administração em. Só é acessível para usuários conectados com um de 2. /adminroleid .Resolva o laboratório acessando o painel de administração e usando-o para excluir o usuário . carlos. Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Vamos acessar o nosso laboratorio e iremos no nosso pergil vamos alterar o nosso email, para facilitar nessa etapa deixaremos em intercept on.

Vamos enviar a requisição para o repeater.

![image](https://user-images.githubusercontent.com/95362045/168655134-f6c84be1-55a1-471b-99a3-35c533dd5340.png)

Vamos pegar a informação roleid: 1 e inserir ao lado do email.

![image](https://user-images.githubusercontent.com/95362045/168655505-2cf8f04d-025a-474d-b1f8-ae1db01b4946.png)

![image](https://user-images.githubusercontent.com/95362045/168655841-478f18bc-b25a-49ec-af42-4a8119ee34e9.png)

O painel administrativo apareceu.

![image](https://user-images.githubusercontent.com/95362045/168656242-9b99876d-8457-4cff-aeaa-64220bd4afea.png)

E agora é só deletar o usuário solicitado :)

## 5. ID do usuário controlado por parâmetro de solicitação

Este laboratório tem uma vulnerabilidade de escalonamento de privilégios horizontais na página da conta de usuário.

Para resolver o laboratório, obtenha a chave de API para o usuário e envie-a como solução. carlos. Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Nós iremos tentar o acesso a conta do carlos ou pegar informações de dentro de nossa conta, isso é escalonamento horizontal. Iremos normalmente acessar a nossa conta.

![image](https://user-images.githubusercontent.com/95362045/171204169-670df9d9-c90e-4ed3-a5c8-17fc9cfc3dcb.png)

Agora iremos clicar em my-account e iremos pegar a requests e iremos analisar. No cabeçalho GET podemos que o usuário é definido por um ID que mostra a conta que estamos, porém e se colocarmos outro nome com a intenção de levar a um ID de outro usuário ? Vamos realizar esse teste trocando wiener por carlos e enviaremos para o repeater.

![image](https://user-images.githubusercontent.com/95362045/171204504-dda7e773-e42a-48b2-828c-54d70adf76ff.png)

Aqui é a request e a response da troca que realizamos.

![image](https://user-images.githubusercontent.com/95362045/171204860-ee81ffd5-c1ae-430f-86f8-4a1d1a59a401.png)

Descendo mais um pouco na resposta podemos ver a API key de carlos. Agora é só copiar e colocar e finalizar a lab 

![image](https://user-images.githubusercontent.com/95362045/171205986-ce9cf154-9680-4911-a0fd-87c0292cd155.png)

![image](https://user-images.githubusercontent.com/95362045/171205344-0b92af0f-fa3e-4086-b868-97556e44c45f.png)

## 6. ID do usuário controlado por parâmetro de solicitação, com IDs de usuário imprevisíveis

Este laboratório tem uma vulnerabilidade de escalonamento de privilégios horizontais na página da conta de usuário, mas identifica usuários com GUIDs.

Para resolver o laboratório, encontre o GUID para, em seguida, envie sua chave de API como a solução. carlos

Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Esse labortório é bem parecido com o antetior mas ele ao inves de definir o nome do usuário como ID ele identifica usuáqrios como GUIDs. Vamos fazer o mesmo procedimento de se logar com a conta wiener:petter,e iremos acessar a nossa conta. Aqui nesta imagem podemos ver a nossa API Key. 

![image](https://user-images.githubusercontent.com/95362045/171215761-aa9dcccb-5c80-4744-922f-0e38fda828ba.png)

Encontrando o post de carlos iremos clicar sobre o nome dele e ver a request.

![image](https://user-images.githubusercontent.com/95362045/171220291-22f453f8-4752-4fc5-b21a-bcb2c679e288.png)

Vamos copiar e vamos acessar my-account e vamos pegar a request. Vamos apagar o nosso id e vamos inserir a do carlos. E clicar em forward.

![image](https://user-images.githubusercontent.com/95362045/171222811-22972371-0440-4ff2-b9fb-ac23e924885f.png)

Agora conseguimos ter acesso aconta do carlos e temos a API Key. Agora vamos copiar e colar e finalizar a lab.

![image](https://user-images.githubusercontent.com/95362045/171223140-14047e28-52bb-4ce4-a375-5ab23e06fd55.png)

![image](https://user-images.githubusercontent.com/95362045/171223304-56b464e7-19f4-41d2-b663-d76443f29e1c.png)

## 7. ID do usuário controlado por parâmetro de solicitação com vazamento de dados no redirecionamento

Este laboratório contém uma vulnerabilidade de controle de acesso onde informações confidenciais são vazadas no corpo de uma resposta de redirecionamento.
Para resolver o laboratório, obtenha a chave de API para o usuário e envie-a como solução. carlos. Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Acessando o nosso laboratório iremos realizar o nosso login, posteriormente iremos acessar a aba my-account e vamos pegar essa requisição e envia-lá para o repeater

![image](https://user-images.githubusercontent.com/95362045/171476838-29859458-2ce9-4fd0-9e7b-40489d2be225.png)

Agora iremos modificar o Id e colocaremos carlos no lugar do wiener. Depois de clicar em send podemos perceber na response que fomos redirecionados (302) para a área de login.

![image](https://user-images.githubusercontent.com/95362045/171477189-bd975838-d06d-4e41-bf8b-71a56317937f.png)

Analisando melhor o body da response podemos perceber alguns detalhes. Mesmo redirecionando ele nos trás a api key do usuário carlos.

![image](https://user-images.githubusercontent.com/95362045/171477635-213008c1-eb3f-47b8-a3ee-b15724f330e0.png)

![image](https://user-images.githubusercontent.com/95362045/171478740-de41ca33-227b-4b73-9065-7f0f8d291004.png)

## 8. ID do usuário controlado por parâmetro de solicitação com divulgação de senha

Este laboratório tem uma página de conta de usuário que contém a senha existente do usuário atual, pré-preenchida em uma entrada mascarada.

Para resolver o laboratório, recupere a senha do administrador e use-a para excluir . carlos

Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Esse laboratório tem a mesma lógica que o exercício anterior, iremos acessar com a nossa conta e pegar a request quando acessamos a aba My account.

![image](https://user-images.githubusercontent.com/95362045/171483456-f38a01b6-a3a9-4f2c-9978-a1f53fd82989.png)

Agora antes de acessar a conta de administrador vamos acessar a conta do carlos, iremos mudar o parametro id para carlos e clicar em forward. Podemos ver que ele nos trás a senha de um ouro usuário mascarado, na verdade acessamos a conta de um outro usuário.

![image](https://user-images.githubusercontent.com/95362045/171483997-0429b92c-6ac7-444a-bca6-50833124873c.png)

Agora iremos voltar ao passo anterior e iremos modificar o parametro para administrator e clicar em forward.

![image](https://user-images.githubusercontent.com/95362045/171484451-7dc1811a-fa94-4656-bd2b-c2e9120fae3f.png)

Agora para descobrirmos qual é a senha podemos utulizar um metodo que é no HTML da pagina, vamos realizar a marcação da senha mascarada e iremos clicar em inspecionar, desta maneira.

![image](https://user-images.githubusercontent.com/95362045/171484710-65690adb-87ed-4e56-a354-7e42b273ad0a.png)

Agora ali no input required type="password" vamos modificar substituindo por "text" isso vai fazer o tipo da inserção vire do tipo texto e não senha. Ficando desta forma.

![image](https://user-images.githubusercontent.com/95362045/171484949-4664a2ed-bcae-40a3-a0f2-30b8f5a806fb.png)

Agora sabendo a senha iremos logar com o usuário: administrator senha: 4daft2pq8cj1d03xt9nq, e iremos em admin panel e deletar o usuário carlos.

![image](https://user-images.githubusercontent.com/95362045/171485319-441fe4e2-5ffe-4c5d-be96-bac0dc4f7748.png)

Tarefa concluida

![image](https://user-images.githubusercontent.com/95362045/171485333-a059f535-50a3-4ca2-9ee3-b67679b71480.png)

## 9. Insecure direct object references

Este laboratório armazena registros de bate-papo do usuário diretamente no sistema de arquivos do servidor e os recupera usando URLs estáticas. Resolva o laboratório encontrando a senha para o usuário e fazendo login em sua conta. carlos

Vamos entrar no nosso laboratório, ao acessar iremos em live chat, sinalizado no canto superior direito, e ao entrar iremos mandar qualquer mensagem.

![image](https://user-images.githubusercontent.com/95362045/171639395-45e12bba-5668-4885-9d74-7b2a8c4f373d.png)

Feito isso iremos deixar no burp a opção de intercept on e vamos pegar acessar view transcript. Vamos clicar em forward até chegar nessa request.

![image](https://user-images.githubusercontent.com/95362045/171639787-cf5908d1-8ee5-48ab-af76-6894724f2d43.png)

 Agora iremos realizar uma modificação e colocaremos 1.txt e clicar em forward.
 
 ![image](https://user-images.githubusercontent.com/95362045/171639925-7f28bd11-f5fd-43e3-b0bc-c6fd06729dba.png)
 
 Ele gerou um arquivo e nele consta o password. Agora é só copiar e logar com a conta de carlos e finalizar a lab.
 
 ![image](https://user-images.githubusercontent.com/95362045/171640180-c704adbc-e1b1-467d-99d5-163cff052408.png)

![image](https://user-images.githubusercontent.com/95362045/171640288-2103445b-6d92-4752-9a30-6e90caf7b896.png)

