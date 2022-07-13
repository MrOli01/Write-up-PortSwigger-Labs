# XML external entity (XXE) injection

## Lab: Exploiting XXE using external entities to retrieve files

Este laboratório tem um recurso "Verificar estoque" que analisa a entrada XML e retorna quaisquer valores inesperados na resposta. Para resolver o laboratório, injete uma entidade externa XML para recuperar o conteúdo do arquivo. /etc/passwd

Vamos acessar o laboratório e vamos clicar em algum produto, clicaremos em verificar estoque, vamos interceptar a solicitação POST resultando no Burp.

![image](https://user-images.githubusercontent.com/95362045/169540607-2e192d9c-6126-4178-b6b8-2eed2a6ca133.png)

Vamos realizar umas modificações, vamos definir uma entidade externa entre a declaração XML e o elemento stockcheck ficando desta forma.

Esta carga XXE define uma entidade externa cujo valor é o conteúdo do arquivo e utiliza a entidade dentro do valor. Isso faz com que a resposta do aplicativo inclua o conteúdo do arquivo

![image](https://user-images.githubusercontent.com/95362045/169541258-babb82c4-ac76-483f-8f9f-9dc4b94b5bc8.png)

E podemos depois de clicar em Forward podemo ver que conseguimos concluir a lab.

![image](https://user-images.githubusercontent.com/95362045/169541750-8a22622c-ba3d-421f-8d20-17b78e69ee4f.png)

## 2. Exploiting XXE to perform SSRF attacks

Este laboratório tem um recurso "Verificar estoque" que analisa a entrada XML e retorna quaisquer valores inesperados na resposta. O servidor de laboratório está executando um ponto final (simulado) de metadados EC2 na URL padrão, que é . Este ponto final pode ser usado para recuperar dados sobre a instância, alguns dos quais podem ser sensíveis. http://169.254.169.254/ Para resolver o laboratório, explore a vulnerabilidade XXE para realizar um ataque SSRF que obtenha a chave de acesso secreto IAM do servidor a partir do ponto final de metadados EC2.

Vamos acessar o laboratório e verificar o estoque de algum produto.

![image](https://user-images.githubusercontent.com/95362045/169545592-665fe96d-6e6d-44be-a077-fc2855906258.png)

Agora vamos realizar essas modificações.

![image](https://user-images.githubusercontent.com/95362045/169546180-89e6a7e2-8bc5-4e49-844a-c9a6fc65319a.png)


