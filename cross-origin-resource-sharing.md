Cross-origin resource sharing (CORS)

 ## 1. Lab: CORS vulnerability with basic origin reflection

Este site tem uma configuração CORS insegura na sua confiança em todas as origens. Para resolver o laboratório, crie um JavaScript que use CORS para recuperar a chave de API do administrador e carregue o código para o servidor de exploração. O laboratório é resolvido quando você envia com sucesso a chave API do administrador.
Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

O CORS (Cross-origin Resource Sharing, compartilhamento de recursos de origem cruzada) é um mecanismo de navegador que permite o acesso controlado aos recursos localizados fora de um determinado domínio. Estende-se e adiciona flexibilidade à política de mesma origem (SOP). No entanto, ele também fornece potencial para ataques entre domínios, se a política cors de um site estiver mal configurada e implementada. O CORS não é uma proteção contra ataques de origem cruzada, como falsificação de solicitação entre sites (CSRF). 

Já que temos agora uma visão do que é o CORS iremos acessar nosso laboratório e logar com o wiener:peter

![image](https://user-images.githubusercontent.com/95362045/168606135-c8146406-ba54-4689-99bc-04a0f4365e81.png)

Agora vamos olhar o HTTP History ( GET /accountDetails) e ver que a nossa chave é recuperada através de uma solicitação AJAX e a resposta contém o cabeçalho sugerindo que pode suportar CORS:

![image](https://user-images.githubusercontent.com/95362045/168608835-90d93d49-9790-4446-b357-b9c8f798b3b5.png)

Agora na request vamos adicionar um header origin: https//exemple.com

![image](https://user-images.githubusercontent.com/95362045/168609992-f14f250e-73e6-41f0-8860-c8661de40f9f.png)

Observe que a origem se reflete no cabeçalho. Access-Control-Allow-Origin. No navegador iremos para o servidor de exploração e digite o SEGUINTE HTML, substituindo-o pela sua URL de laboratório exclusiva: $url

Agora iremos desenvolver um script em JS

![image](https://user-images.githubusercontent.com/95362045/168610809-92f3a9d3-8e14-4b7a-a82d-523e64bcf887.png)

depois de substituir a URL, vammos agora clicar em deliver exploit to victim. e posteriormente vamos acessar o log.

![image](https://user-images.githubusercontent.com/95362045/168616435-5dd4ae76-5a4b-46d5-b219-87efe6078122.png)

Podemos ver que conseguimos capturar os dados do administrador, vamos ir até a apikey e copia-lá e finalizar a challenge.

![image](https://user-images.githubusercontent.com/95362045/168617316-bc54240e-a766-4ec5-acda-fe818e96468e.png)

## 2. Lab: CORS vulnerability with trusted null origin

Este site tem uma configuração CORS insegura na sua confiança na origem "nula". Para resolver o laboratório, crie um JavaScript que use CORS para recuperar a chave de API do administrador e carregue o código para o servidor de exploração. O laboratório é resolvido quando você envia com sucesso a chave API do administrador.
Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Vamos realizar o login no nosso laboratório usando wiener:peter no burp suite

![image](https://user-images.githubusercontent.com/95362045/169347408-ba153164-834f-4bad-8abe-538b121d8856.png)

Agora indo em HTTP History vamos observar que a nossa chave é recuperada através de uma solicitação AJAX e a resposta contém o cabeçalho sugerindo que ele suporta o CORS 

![image](https://user-images.githubusercontent.com/95362045/169351490-a1fca5a0-528d-4f0d-b662-519251270875.png)

Vamos agora enviar a request para o repeater e iremos adicionar no cabeçalho origin: null.

![image](https://user-images.githubusercontent.com/95362045/169352526-051f2fac-2cf3-4746-bfbc-ce219cb64c63.png)

Ao clicar em send podemos ver que a origin: null reflete no cabeçalho Access-Control-Allow-Origin

![image](https://user-images.githubusercontent.com/95362045/169352880-24f28253-9316-43ab-a117-e0794d68462a.png)

Agora vamos para o navegador e iremos ir em servidor de exploração evamos fazer um html.

![image](https://user-images.githubusercontent.com/95362045/169354056-e4fc0b94-2ed6-4399-94e8-61349a2aa68d.png)

Vai estar desta maneira, em req.open você colocara sua URL exclusiva do laboratório e em location você colocara a URL do seu servidor de exploit. Depois disso é só clicar em store e depois vão clicar em deliver exploit que vai ser para encaminhar para a vítima e clicar posteriormente em Access log

![image](https://user-images.githubusercontent.com/95362045/169355950-cfea02b8-e5f1-44b8-9668-7f8a554dc84b.png)

Vamos copiar toda a linha e vamos ao burp na área decoder. Vamos colar o que copiamos e vamos clicar em smart decode.

![image](https://user-images.githubusercontent.com/95362045/169358005-c3c5447b-e259-4a44-b19b-c3e16314b26a.png)

Vamos copiar a apikey e vamos ir até o nosso laboratório finalizar a nossa lab.

![image](https://user-images.githubusercontent.com/95362045/169358312-5dfabc0e-7c3a-4fdb-820d-be993610ffa0.png)
