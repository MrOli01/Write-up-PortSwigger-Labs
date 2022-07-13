# Insecure deserialization

## 1. Lab: Modifying serialized objects

Este laboratório usa um mecanismo de sessão baseado em serialização e é vulnerável a uma escalada privilegiada como resultado. Para resolver o laboratório, edite o objeto serializado no cookie da sessão para explorar essa vulnerabilidade e obter privilégios administrativos. Então, exclua a conta do Carlos.

Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Nesse laboratório iremos fazer o login com o usuário wiener:peter, postreriormente a isso iremos analisar a requisição /my-account.

![image](https://user-images.githubusercontent.com/95362045/172183460-d994ff2c-ea20-4226-b6ab-5106613e3484.png)

Feito isso iremos verificar com o cookie de sessão com o inspetor ao lado direito. Podemos ver que é um PHP serializado. E iremos pegar essa request e enviar para o repeater.

![image](https://user-images.githubusercontent.com/95362045/172183622-388f00cc-3124-4038-9c5e-6f9cc59ddaad.png)

Já em repeater iremos fazer uma modificação, em inspetor iremos modificar o 0 por 1, que está indicado como um valor boleano, e logo em seguida vamos aplicar essas modificações.

![image](https://user-images.githubusercontent.com/95362045/172184150-7d09f899-f75b-4bcd-91bf-be5d861654a9.png)

![image](https://user-images.githubusercontent.com/95362045/172184203-bf5ad917-686b-4d8a-96ce-c8f731be214c.png)

Feito isso vamos clicar em send e verificar o que ele nos retorna.Temos um status code 200 OK e descendo mais um pouco podemos ver que ele nos trás o encaminhamento para o painel administrativo. 

![image](https://user-images.githubusercontent.com/95362045/172184503-c36cfc1d-bd5b-4941-9bfd-164ab1f420d5.png)

Agora iremos modificar o caminho para /admin, e depois vamos ir na guia request in browser (in original session) Na janela ao lado já podemos perceber que temos permissões administrativas para deletar o usuário carlos.

![image](https://user-images.githubusercontent.com/95362045/172184863-d43b07ed-5559-467d-a19d-b2f87fdef06f.png)

Agora é só clicar em deletar no usuário carlos e verificar a request, vamos realizar novamente a mudança de 0 para 1 e clicar em forward e finalizar a lab.

![image](https://user-images.githubusercontent.com/95362045/172185802-75dbcbc6-331d-48db-8757-63dbc9926f01.png)

