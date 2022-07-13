# WebSockets

## 1. Manipulação de mensagens do WebSocket para explorar vulnerabilidades

Esta loja online tem um recurso de bate-papo ao vivo implementado usando WebSockets. As mensagens de bate-papo que você envia são visualizadas por um agente de suporte em tempo real.
Para resolver o laboratório, use uma mensagem do WebSocket para ativar um popup no navegador do agente de suporte. alert()

Vamos acessar nosso laboratório e clicar em chat. 

![image](https://user-images.githubusercontent.com/95362045/171884712-5990960a-4186-42bf-bdf1-362bd5f24fb3.png)

Iremos agora digitar qualquer coisa e clicar em send e vamos analisar essa requests.

![image](https://user-images.githubusercontent.com/95362045/171885036-ed6e6d1d-9fad-43e6-892d-1b4180c6374d.png)

Vamos agora acessar a guia de web sockets history. Podemos ver em que está marcado o encaminhamento da nossa  mensagem para o servidor.

![image](https://user-images.githubusercontent.com/95362045/171886493-fff8b5db-47c5-4c99-80f9-13d55abce1f5.png)

Iremos nesse momento mandar para o repeater e realizar algumas modificações. Vamos substituir o Hello por um script ficando desta forma

![image](https://user-images.githubusercontent.com/95362045/171889250-0a803a71-ed57-4ebd-8268-4ca05951bb83.png)

Agora é só clicar em reconect e clicar em send e verificar. Voltando ao navegador podemos ver que concluimos a tarefa.

![image](https://user-images.githubusercontent.com/95362045/171889886-c02bfb56-7a1e-4718-838e-053a21d1d452.png)

![image](https://user-images.githubusercontent.com/95362045/171890881-553cf395-d56f-41e2-bac3-c9b5f62dc324.png)
