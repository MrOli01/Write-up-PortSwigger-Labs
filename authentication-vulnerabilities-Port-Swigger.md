# Authentication vulnerabilities


 ## 1. Lab: Username enumeration via different responses
 
Este laboratório é vulnerável a enumerações de nomes de usuário e ataques de força bruta por senha. Ele tem uma conta com um nome de usuário e senha previsíveis, que podem ser encontradas nas seguintes listas de palavras:

Para resolver o laboratório, enumerar um nome de usuário válido, forçar a senha desse usuário e acessar a página da conta.

Como dito anteriormente devemos enumerar os usuários válidos e forças suas senhas até ter o acesso. Neste laboratório o site disponibiliza uma lista de usuários e senhas, então usaremos essas informações. 

![image](https://user-images.githubusercontent.com/95362045/167898971-8f703fac-7410-4e40-9eb4-60519cfeadcc.png)

![image](https://user-images.githubusercontent.com/95362045/167899007-6df8e939-455d-4a00-b430-37a073fabb63.png)

Iremos criar 2 arquivos txt, podemos nomear ele conforme preferência pessoal, mas como é comum iremos nomear como wordlist_usuarios.txt e wordlist_senhas.txt. Iremos pegar os nomes e senhas no site e colocar em seus respectivos arquivos. Ou também poderá ser feito copiando os usuários e senhas direto do site, ao invés de selecionar o arquivo em sí será preciso apenas copiar e colar.

Agora que temos nossa wordlist montada poderemos acessar o nosso laboratório. Podemos perceber que é o mesmo site dos exercícios anteriores, agora vamos acessar my account e veremos que é uma janela simples de login e aparentemente não requer MFA, será mais fácil de uma força bruta.

![image](https://user-images.githubusercontent.com/95362045/167900050-db04bd78-f507-4caf-8215-54af6e5b3370.png)

Vamos acessar o nosso burpSuite. Vamos usar o navegador padrão. Já interceptando a página do laboratório vamos realizar um teste aleatório para saber como funciona a requisição do login.

![image](https://user-images.githubusercontent.com/95362045/167900639-8d55a537-363d-4829-8d6c-b36535c78a5e.png)

Podemos ver que na linha 23 ele nos trás os parâmetros username e password. Se você for analisar ele trás o mesmo usuário e senha no teste. Já entendendo como funciona vamos mandar essa requisição para o intruder, indo até o mesmo iremos dar um clear$, Será mais fácil identificarmos qual usuário é valido para depois realizar uma força bruta com as senhas, vamos marcar a resposta do parametro username e definir o attack type como sniper.

Após finalizar a wordlist vamos diferenciar o tempo de resposta.

![image](https://user-images.githubusercontent.com/95362045/167911482-4576c273-d57f-4b17-9994-a7012b6b97d6.png)

Como todos estão nos trazendo status code 200 vamos analisar o tempo de resposta, e o único diferente é o usuário puppet e para confirmar podemos abrir o response

![image](https://user-images.githubusercontent.com/95362045/167911697-023c9aff-7a89-49e1-8d5e-41aa9f955d3c.png)

Aqui está nos informando que a senha está incorreta e não o usuário. Agora vamos definir o primeiro parâmetro username (puppet) e setar a wordlist de senha e efetuar o mesmo procedimento. Após feito os testes encontramos uma senha football com status 302 e com tempo curto de resposta.

![image](https://user-images.githubusercontent.com/95362045/167913425-daafa4d9-aba3-4412-8a65-8dd2a15fafd4.png)

E aqui conseguimos acesso com usuário puppet e senha? football
![image](https://user-images.githubusercontent.com/95362045/167913706-ba4d1d0e-d138-4e19-9126-434bbc524b69.png)


# Authentication vulnerabilities


 ## 2. Lab: 2FA simple bypass
 
 Às vezes, a implementação da autenticação de dois fatores é falha ao ponto de ser contornada completamente.

Se o usuário for solicitado a digitar uma senha e, em seguida, solicitado a inserir um código de verificação em uma página separada, o usuário está efetivamente em um estado de "login" antes de ter inserido o código de verificação. Vamos aplicar isso nessa lab. A atividade diz o seguinte:

Às vezes, a implementação da autenticação de dois fatores é falha ao ponto de ser contornada completamente. Se o usuário for solicitado a digitar uma senha e, em seguida, solicitado a inserir um código de verificação em uma página separada, o usuário está efetivamente em um estado de "login" antes de ter inserido o código de verificação.

Assim que acessarmos o laboratório vamos inserir nosso usuário e senha que é wiener:peter.

![image](https://user-images.githubusercontent.com/95362045/167932191-dcf453ec-ad73-41e7-ba96-d47caf9a27a4.png)

Após isso será solicitado um código de 4 números, iremos acessar Email client, que está no centro superior da página, ao acessar iremos pegar o código e inserir no local que pede. Após a confirmação podemos ver que nossa URL muda no final (my-aacount)

![image](https://user-images.githubusercontent.com/95362045/167932769-4322382d-e367-43d9-a0bc-624e4ea99280.png)

Agora iremos acessar a conta do usuário carlos, a senha do mesmo é montoya. Quando solicitar em uma outra página os códigos iremos fazer uma alteração na URL, onde está escrito /login2 iremos substituir por /my-account 

![image](https://user-images.githubusercontent.com/95362045/167933107-db799f20-8528-4c5c-bcff-c512c0e4343e.png)

Neste caso, vale a pena testar para ver se você pode pular diretamente para páginas "somente logd-in" depois de completar a primeira etapa de autenticação. Ocasionalmente, você verá que um site não verifica se você completou ou não o segundo passo antes de carregar a página.



 




