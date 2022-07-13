# Web shell upload

 ## 1. Remote code execution via web shell upload
 
Este laboratório contém uma função de upload de imagem vulnerável. Ele não executa nenhuma validação nos arquivos que os usuários carregam antes de armazená-los no sistema de arquivos do servidor. Para resolver o laboratório, carregue um web shell básico php e use-o para exfiltrar o conteúdo do arquivo . Envie este segredo usando o botão fornecido no banner do laboratório. /home/carlos/secret. Você pode fazer login usando as seguintes credenciais: wiener:peter

Iremos realizar essa atividade usando o burp suite e o seu navegador padrão. Vamos realizar o login usando os usuário e senha citado a cima. 

![image](https://user-images.githubusercontent.com/95362045/167711946-0bea2ebe-e8dc-48ca-8bdd-f7f289a10788.png)

Feito isso podemos perceber que possui uma área de upload de arquivo para seu avatar. Realizaremos em um bloco de notas um script php para exfiltrar arquivos do servidor.
O script ficara desta forma podera ser salvo como shell1.php em qualquer lugar na máquina, por exemplo na área de trabalho.

![image](https://user-images.githubusercontent.com/95362045/167713955-dea3fe35-d8a1-4269-8b26-0e1577d4eee3.png)

Dentro dos "()" estamos definindo o caminho para extrair informações que está localizado em secret. ('/home/calors/secret')

Agora iremos intereptar as requisições e selecionar o arquivo e cliar com upload. No burp podemos ver a requisição de envio do arquivo e clicando em forward e indo ao navegador conseguimos ver que o upload do arquivo foi bem sucecido.

![image](https://user-images.githubusercontent.com/95362045/167715052-92c349b4-9084-486b-8dc8-2d8b55e66c50.png)

Podemos parar a interceptação e posteriormente vamos em HTTP History. Podemos no momento selecionar o my-account/avatar e encaminhar ela para o repeater.

![image](https://user-images.githubusercontent.com/95362045/167715494-b7fc666f-23c5-4aca-b5c1-28189cb69885.png)

Realizamos uma alteração no caminho da solicitação para apontar o nosso arquivo php

![image](https://user-images.githubusercontent.com/95362045/167715955-c50ccf44-7597-45d1-9136-19e7a9510de8.png)

![image](https://user-images.githubusercontent.com/95362045/167715997-36d339e1-61c7-465f-9f5b-5e5693d9e5b8.png)

E aqui temos a response e o segredo, agora é só copiar a mesma e finalizar a challenge.

# Web shell upload

 ## 2. Web shell upload via Content-Type restriction bypass
 
Para resolver o laboratório, carregue um web shell básico php e use-o para exfiltrar o conteúdo do arquivo . Envie este segredo usando o botão fornecido no banner do laboratório. /home/carlos/secret

Podemos fazer login em sua própria conta usando as seguintes credenciais: wiener:peter. Diferentemente da primeira lab esse possui um bloqueio ao enviar arquivos que são fora do padrão esperado pelo servidor. Vamos fazer um teste, iremos logar e enviar uma foto qualquer como avatar.

![image](https://user-images.githubusercontent.com/95362045/167870166-2d056050-b937-45e7-96ee-5415c9c47936.png)

Na imagem a seguir é a resposta que o avatar foi enviado com sucesso. 

![image](https://user-images.githubusercontent.com/95362045/167870425-367031ed-81d7-4381-9565-eb089517245a.png)

E de volta a página podemos ver o avatar.

![image](https://user-images.githubusercontent.com/95362045/167870581-930f31f2-225a-412c-ba99-ba7b94a78e83.png)

Agora se tertarmos enviar por exemplo o bloco de notas contendo um script em php iremos receber o seguinte erro: Only image/jpeg and image/png

![image](https://user-images.githubusercontent.com/95362045/167871128-68f763bd-279f-427d-8c25-99d07ade043f.png)

Então iremos burlar essa métrica de segurança. Iremos enviar esse pedido para o repeater

![image](https://user-images.githubusercontent.com/95362045/167882094-88e64ce9-b96e-44dd-b1a5-d8b375bfdf09.png)

E neste momento iremos criar ou pegar o script em php, é o mesmo script do exercício anterior.

![image](https://user-images.githubusercontent.com/95362045/167882449-35a5b528-1ef2-4bd3-be88-2b5f671029ee.png)

Como testamos antes iremos achar a requisição que deu 403 que foi o status code que o arquivo não foi aceito e encaminharemos para o repeater:

![image](https://user-images.githubusercontent.com/95362045/167885877-a162292b-c5d9-4596-a9f1-d4942082b54b.png)

Teremos que fazer uma modificação nesse trecho da requisição. Podemos perceber que está se referindo ao nosso arquivo shell1.php, teremos que realizar a modificação no content-type que serve para indicar qual tipo de arquivo, então colocaremos content-Type: image/jpeg e clicar em send. 

![image](https://user-images.githubusercontent.com/95362045/167887632-39649e39-22ee-4d88-adad-f85364f2e91d.png)

ficando desta maneira:

![image](https://user-images.githubusercontent.com/95362045/167887744-da462aa3-1aff-4be2-bb49-181a8f780838.png)

Recebemos um status code 200 ok. Agora iremos para a solicitação GET. Iremos realizar uma nova modificação, iremos deletar o my-account e substituir por /file/avatars/shell1.php 

![image](https://user-images.githubusercontent.com/95362045/167889515-692d2a1a-7a88-452d-84a6-3a5f432ef840.png)

Agora temos a nossa chave e é só copiar e colocar o código.



