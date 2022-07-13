# Cross-site scripting


 ## 1. Reflected XSS into HTML context with nothing encoded
 
 Este laboratório contém uma simples vulnerabilidade de script de sites refletidos na funcionalidade de pesquisa. Para resolver o laboratório, realize um ataque de scripting entre sites que chama a função. alert
 
 Cross-site scripting refletido também conhecido como XSS refletido, XSS não persistente ou XSS tipo 1, é uma das vulnerabilidades mais encontrada atualmente. Essa falha se manifesta quando a aplicação web vulnerável reflete um valor qualquer, sem antes validá-lo de forma correta

Para realizar uma prova de conceito preguiçosa podemos utilizar um script basico para identificar essa vulnerabilidade. 

<script>alert(1)</script>

Sua principal função é mostrar ao usuário uma mensagem e um botão de confirmação de que o usuário tenha visto a mensagem. O método alert() exibe uma mensagem no navegador por meio de uma caixa de diálogo, que nada mais é que uma pequena janela popup

Iremos acessar nosso laboratório. 

![image](https://user-images.githubusercontent.com/95362045/168295540-e5467a3f-3ba5-4fcf-b974-3132565f8501.png)

Temos apenas uma caixa de entrada que possamos testar nosso script para que identificamos essa vulnerabilidade. 

Vamos copiar nosso script e clicar em search

![image](https://user-images.githubusercontent.com/95362045/168295744-f6a4ccf7-3f26-4d6e-9576-d82e78e47ab7.png)

![image](https://user-images.githubusercontent.com/95362045/168295794-4ea1348d-f8cb-44ab-a0ca-f0c0c926c5d0.png)

Conseguimos :D


 ## 2. Stored XSS into HTML context with nothing encoded
 
Este laboratório contém uma vulnerabilidade de scripting entre sites armazenada na funcionalidade de comentários. Para resolver este laboratório, envie um comentário que chame a função quando o post do blog for visualizado. alert. XSS Armazenado, também conhecido como XSS Persistente, é considerado o tipo de ataque XSS mais prejudicial. O XSS Armazenado ocorre quando a entrada fornecida pelo usuário é armazenada e, em seguida, processada em uma página da Web.

![image](https://user-images.githubusercontent.com/95362045/168297654-1c3a2966-fdc9-4773-86ad-655c118757fb.png)

Etapas de XSS armazenado

Da figura acima

- Um invasor envia o script malicioso na forma de um arquivo.
- Ele é armazenado no banco de dados do site, se o elemento no aplicativo da web não for higienizado
- Usuário normal ou vítima tenta usar a funcionalidade do aplicativo da web, mas os scripts maliciosos são executados porque já estão armazenados no banco de dados e os cookies ou sessão são roubados pelo invasor.

Ao acessar o laboratório devemos identificar a área de comentários visualizando qualquer postagem.

![image](https://user-images.githubusercontent.com/95362045/168298298-c288c2b1-79fa-4a4e-849a-f449e7a81f4e.png)

Vamos digitar no campo de comentários esse seguinte código <script>alert(1)</script> 

E vamos preencher normalmente os restantes dos campos e postar o comentário.

![image](https://user-images.githubusercontent.com/95362045/168300246-be55844d-ffc5-4829-bfcc-be47b771241a.png)

![image](https://user-images.githubusercontent.com/95362045/168300322-8bf837e6-996e-42a0-87b9-347bc43ed433.png)

Logramos êxito no laboratório. Algumas observações devem ser feitas, quando colocar o website deve constar http:// se não irá acusar erro. O teste manual para XSS refletido e armazenado normalmente envolve o envio de alguma entrada única simples (como uma pequena sequência alfanumérica) em cada ponto de entrada do aplicativo, identificando todos os locais onde a entrada enviada é devolvida em respostas HTTP e testando cada local individualmente para determinar se a entrada adequadamente trabalhada pode ser usada para executar javaScript arbitrário. Desta forma, você pode determinar o contexto em que o XSS ocorre e selecionar uma carga útil adequada para explorá-la.

## 3. SDOM XSS in sink using source

Um ataque XSS baseado em DOM é geralmente um ataque do lado do cliente, e a carga maliciosa nunca é enviada ao servidor. Isso torna ainda mais difícil a detecção de WAFs (Web Application Firewalls) e engenheiros de segurança que analisam os logs do servidor porque nunca veem o ataque.

Este laboratório contém uma vulnerabilidade de scripting entre sites baseada em DOM na funcionalidade de rastreamento de consulta de pesquisa. Ele usa a função JavaScript, que grava dados para a página. A função é chamada com dados de , que você pode controlar usando a URL do site. document.writedocument.writelocation.search

Para resolver este laboratório, realize um ataque de scripting entre sites que chama a função. alert

Vamos acessar o nosso laboratório.

Na área de pesquisa do site iremos digitar quaiquer coisas aleatórias e pesquisar. 
 
![image](https://user-images.githubusercontent.com/95362045/168307411-66a801aa-0dba-47a2-9657-8d087af26849.png)

Feito isso iremos em inspecionar e pesquisar o que você digitou.

![image](https://user-images.githubusercontent.com/95362045/168307555-25570ec9-3409-4538-8231-30c874713deb.png)

Vemos aqui que ela é colocada dentro de origem da imagem. agora podemos fechar e voltar para a área de busca.

Lá iremos colocar o seguinte comando e iremos dar enter.

![image](https://user-images.githubusercontent.com/95362045/168307951-e2eea99f-47a9-4cb5-8f71-d55d43c8f096.png)

![image](https://user-images.githubusercontent.com/95362045/168307062-fdde279d-e1f1-4b03-93a1-2d9951157a07.png)

Podemos ver aqui que conseguimos chamar a janela de alert.
 
 ## 4. DOM XSS in sink using source
 
 Este laboratório contém uma vulnerabilidade de scripting cross-site baseada em DOM na funcionalidade do blog de pesquisa. Ele usa uma atribuição, que altera o conteúdo HTML de um elemento, usando dados de . innerHTMLdivlocation.search. Para resolver este laboratório, realize um ataque de scripting entre sites que chama a função. alert

Vamos acessar o nosso laboratório e iremos colocar no campo de pesquisa o seguinte comando:

![image](https://user-images.githubusercontent.com/95362045/168317904-2d6a58ea-d2b4-4098-962c-7bccf4b13705.png)


![image](https://user-images.githubusercontent.com/95362045/168317987-caae0ca5-2d9a-4ea4-997e-036cb8c4e94c.png)

Podemos ver que conseguimos concluir o laboratório, o que fizemos foi uma carga XSS tentndo obter uma mensagem de erro. <img src=1 vai sair como erro pois não está nos trazendo nenhum conteudo, e o evento oneerror ocorre ao carregar um arquivo externo.


## 5. Reflected XSS into a JavaScript string with angle brackets HTML encoded
                                                                                                                             
Este laboratório contém uma vulnerabilidade de scripting transversal refletida na funcionalidade de rastreamento de consulta de pesquisa onde os suportes angulares são codificados. O reflexo ocorre dentro de uma sequência JavaScript. Para resolver este laboratório, execute um ataque de scripting entre sites que sai da sequência JavaScript e chama a função. alert
                                                                                                                             
Vamos acessar o laboratório pelo burp, e ao acessar iremos efetuar uma pesquisa, poderá ser qualquer coisa, e posteriormente vamos pegar essa requisição pelo burp.     Feito isso iremos encaminhas a requisição para o repeater.
                                                                                                                             
No repeater iremos dar um send e na response iremos procurar pela palavra pesquisada.                                                                                                                             
![image](https://user-images.githubusercontent.com/95362045/168323126-cc5f9f82-0763-496a-933f-33785fd20994.png)
                                                                                                                             
Ela está dentro de uma variável em JavaScript, e agora iremos na área de pesquisa inserir o seguinte comando

![image](https://user-images.githubusercontent.com/95362045/168323681-48d21ff6-80c5-48ec-a9c6-54dec32cab88.png)

Ao enviar conseguimos mostrar o alert.
                                                                                                                             
Os traços são interpretados como um sinal de menos, então javascript tenta fazer subtração na string. Então olhe para ele como uma equação matemática:   var searchTerms = - s t ring  vazia menos alerta(1) menos sequência vazia é igual a alerta(1)  Assim, acionando o alerta(1) para executar          
                                                                                                                             
![image](https://user-images.githubusercontent.com/95362045/168323641-91aed863-7d4d-4ee6-83d3-7772d454c21a.png)                                                                                                                            
                                                                                                                             
## 6.  Lab: DOM XSS in jQuery anchor href attribute sink using location.search source
																				
Este laboratório contém uma vulnerabilidade de script de site cross-site baseada em DOM na página de feedback de envio. Ele usa a função seletora da biblioteca jQuery para encontrar um elemento de âncora e altera seu atributo usando dados de . $hreflocation.search. Para resolver este laboratório, faça o alerta de link "back". document.cookie
                                                                                                                             
Vamos primeiramente acessar o nosso laboratório. Logo ao entrar teremos a opção de Submit FeedBack , é nela que iremos clicar.	
                                                                                                                             
![image](https://user-images.githubusercontent.com/95362045/169141078-3c0c18c3-4db4-482b-9af2-3d3b86a5ddd3.png)
                                                                                                                             
Logo em seguida temos acesso a um formulário. na URL iremos alterar o parametrode consulta para um sequencia alfanumerica aleatória.

![image](https://user-images.githubusercontent.com/95362045/169142000-51fe0049-b26e-4ef9-9c9f-162fe30c2450.png)
															     
Logo em seguida iremos em inspecionar elemento e vamos fazer uma busca pelo o que colocamos. E podemos perceber que colocamos um parametro href em uma tag
															     
![image](https://user-images.githubusercontent.com/95362045/169142465-830e3282-ede8-4633-8b80-6ef8edf6e3eb.png)
															     
Agora iremos realizar um teste, vamos realizar uma modificação na URL ficando:
															     
![image](https://user-images.githubusercontent.com/95362045/169142896-b658fe3d-0c09-4210-a67f-be83c4d7fddc.png)
															     
Agora vamos ir no botão Back, e podemos ver que solucionamos a lab.															     
![image](https://user-images.githubusercontent.com/95362045/169143288-da46e034-3162-4e8b-a61e-8a70d70f9be9.png)
															     
## .7 	Lab: Reflected XSS into attribute with angle brackets HTML-encoded
															     
Este laboratório contém uma vulnerabilidade de scripting entre sites refletida na funcionalidade do blog de pesquisa, onde os suportes angulares são codificados por HTML. Para resolver este laboratório, realize um ataque de scripting entre sites que injeta um atributo e chama a função. alert                                                                                                                             
Desta vez iremos utilizar o bup para interceptar uma solicitação de pesquisa que iremos fazer, vai ser uma sequência aleatória alfanumérica na caixa de pesquisa.
Então vamos ir até o burp e vamos acessar o nosso laboratório.	
															     
Vamos realizar essa pesquisa, e vamos olhar a response para o repeater.
															     
![image](https://user-images.githubusercontent.com/95362045/169144740-59daf47c-3a0b-405a-94bb-2d069cbbb3b8.png)
															     
![image](https://user-images.githubusercontent.com/95362045/169145565-5a5fa4cf-ccae-4204-9cc3-cfea25d1488c.png)

Agora vamos injetar 	
															     
![image](https://user-images.githubusercontent.com/95362045/169145948-9dc535c5-5494-472a-8b75-49be609ffa05.png)
															     
Podemos abrir em um navegador indo em request in browser ou copiar o comando e injetar diretamente no site. E ao enviar o exercício já estará concluido															     
## 8. Lab: Stored XSS into anchor attribute with double quotes HTML-encodedhref
															     
Este laboratório contém uma vulnerabilidade de scripting entre sites armazenada na funcionalidade de comentários. Para resolver este laboratório, envie um comentário que chame a função quando o nome do autor do comentário for clicado. alert
															     
Vamos acessar o nosso laboratório e iremos realizar um comentário com uma sequencia aleatória na entrada "site" e vamos usar o burp para interceptar a requisição e enviala para o repeater.
															     
![image](https://user-images.githubusercontent.com/95362045/169305596-3ec08e61-78c3-4754-8eeb-cb44b7227234.png)

Vamos pegar também a solicitação do navegador para visualizar o comentário e iremos intercepitar e mandar para o repeater. Aqui podemos ver que ela é armazenada em website.
															     
![image](https://user-images.githubusercontent.com/95362045/169307659-82d17594-a9e1-428e-a45e-01a4b4aa8256.png)
															     
Vamos agora apagar o que escrevemos e vamos colocar javascript:alert(1) e vamos clicar em send.
															     
![image](https://user-images.githubusercontent.com/95362045/169308404-d1bb436e-1791-49da-bb06-ba8af6222b90.png)
														
Após ter alterado vamos clicar em send e posteriormente vamos clicar em follow redirection ao lado do send.
															     
![image](https://user-images.githubusercontent.com/95362045/169309621-495c221d-0d7b-4972-851f-41dc0bb082c0.png)
															     
Agora indo ao laboratório podemos ver que conseguimos finalizar.
															     
![image](https://user-images.githubusercontent.com/95362045/169309793-f86a9820-f871-4b23-8b1c-5c7a69beb583.png)
															     
														     
