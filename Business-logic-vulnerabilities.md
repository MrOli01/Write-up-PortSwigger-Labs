# Business logic vulnerabilities

## 1. Lab: Excessive trust in client-side controls

Este laboratório não valida adequadamente a entrada do usuário. Você pode explorar uma falha lógica em seu fluxo de trabalho de compra para comprar itens por um preço não intencional. Para resolver o laboratório, compre uma "jaqueta de couro leve l33t". Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Vamos acessar o nosso laboratório com o burp e realizar o login. Posteriormente iremos clicar em qualquer produto

![image](https://user-images.githubusercontent.com/95362045/169583949-b69a4683-4950-4a91-a19b-e75b06e5764b.png)

Depois disso vamos tentar comprar a jaqueta, mas a ordem é rejeitada pois não temos créditos o suficiente.

![image](https://user-images.githubusercontent.com/95362045/169584914-a4cea48a-a692-49e9-aa64-3ba2afd97371.png)

Agora iremos até o burp em HTTP history e vamos ver a ordem. conseguimos observar que quando adicionamos algum item no carrinho a solicitação correspondente contém um parametro. Vamos enviar o pedido para o repeater.

![image](https://user-images.githubusercontent.com/95362045/169586344-cad042fd-4a74-4709-8094-e78a563369a9.png)

Agora vamos no repeater e vamos mudar para um preço inteiro arbitrário e vamos enviar o pedido. Vamos atualizar o carrinho e confirmar que o preço foi alterado.

![image](https://user-images.githubusercontent.com/95362045/169586800-9d7c2ba2-9c4c-417d-ad8c-68226d67099c.png)

Podemos ver que o preço foi alterado. Agora é só concluir a compra e finalizar o laboratório 

![image](https://user-images.githubusercontent.com/95362045/169586937-261788e1-3dc3-45d1-a8c2-b59f508b3f80.png)

## 2. Lab: High-level logic vulnerability

Este laboratório não valida adequadamente a entrada do usuário. Você pode explorar uma falha lógica em seu fluxo de trabalho de compra para comprar itens por um preço não intencional. Para resolver o laboratório, compre uma "jaqueta de couro leve l33t". Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Vamos acessar o nosso laboratório com o burp e ao realizar o login vamos colocar algum produto de valor baixo no carrinho.

![image](https://user-images.githubusercontent.com/95362045/170061267-d3919fa9-fa61-4ebd-8ffa-ab0b1c1fb280.png)

Agora iremos em http history e vamos ver as mensagens HTTP correspondentes, o que precisamos analisar é a request com o cabeçalho POST/cart.

![image](https://user-images.githubusercontent.com/95362045/170061793-1155dabb-6503-4c04-995b-e182942b6b35.png)

![image](https://user-images.githubusercontent.com/95362045/170068337-d98ddfd8-051b-4b9b-ad55-916119e80daa.png)


Essa é a request quando realizamos a inserção de um produto no carrinho e podemos ver que a quantidade é determinada por um parâmetro. Agora iremos fazer a mesma coisa com a interceptação em modo on. Vamos mudar o parâmetro para um numero arbitrário e vamos encaminhar as solicitações restantes, depois conseguiremos observar que a quantidade no carrinho foi atualizada com sucesso.

![image](https://user-images.githubusercontent.com/95362045/170063528-5cb4cf4d-9c6a-44aa-86bd-b6ee4ab53280.png)

Agora iremos repetir esse processo mas iremos colocar valores negativos. definimos -600

![image](https://user-images.githubusercontent.com/95362045/170064190-64ce2332-1807-45ba-bfc1-c53878b74ef9.png)

Agora vamos solicitar uma quantidade negativa adequada para remover mais unidades que tem no carrinho. E posteriormente vamos perceber que o valor tambem estará negativo.

![image](https://user-images.githubusercontent.com/95362045/170064795-14900bf3-004b-486f-9496-17b49873ca12.png)

Vamos adicionar a jaqueta de couro ao nosso carrinho normalmente, e vamos adicionar uma quanidade negativa adequada do outro item para reduzir o preço total para menos que o crédito restante da loja. 

![image](https://user-images.githubusercontent.com/95362045/170067896-674e64d5-1889-4a75-9b1a-90e5e198ff49.png)

Agora iremos realizar a compra e concluir a lab

![image](https://user-images.githubusercontent.com/95362045/170068025-6f91738b-6c6e-491f-9c47-afcc92b20fc9.png)

## 3. Lab: Inconsistent security controls

A lógica falha deste laboratório permite que os usuários arbitrários acessem funcionalidades administrativas que só devem estar disponíveis para os funcionários da empresa. Para resolver o laboratório, acesse o painel de administração e exclua Carlos.

## 4. Aplicação falha das regras de negócios

A lógica falha deste laboratório permite que os usuários arbitrários acessem funcionalidades administrativas que só devem estar disponíveis para os funcionários da empresa. Para resolver o laboratório, acesse o painel de administração e exclua Carlos.

Esse laboratório você cria um usuário com o email disponibilizado pela lab, posteriormente você verá que não tem permissões administrativas, mas se você realizar a modificação do dominio que a empresa usa ela não verifica a veracidade se você é realmente funcionario e te da permissão administrativa, e você pode deletar o usuário carlos.

Este laboratório tem uma falha lógica em seu fluxo de trabalho de compra. Para resolver o laboratório, explore essa falha para comprar uma "jaqueta de couro Leve L33t".
Você pode fazer login em sua própria conta usando as seguintes credenciais: wiener:peter

Acessando o nosso laboratório percebemos que para novos clientes tem um cupom NEWCUST5

![image](https://user-images.githubusercontent.com/95362045/170088991-a42f365f-f5ea-482e-a13e-09a09faf8d99.png)

E mais na parte inferior do site podemos ver uma área que é para cadastro para receber novos emails. E quando se cadastra conseguimos mais um cupom, vamos fazer o teste.

![image](https://user-images.githubusercontent.com/95362045/170089286-09744c64-a5a7-487c-813a-58bfbce65409.png)

Coloque qualquer email e verá um pop-up com o cupom.

![image](https://user-images.githubusercontent.com/95362045/170089436-fd5a878b-9776-4938-bf15-ce9eea74819b.png)

Feito isso iremos colocar no carrinho a nossa jaqueta e iremos acessar a área de inserção dos cupons.

![image](https://user-images.githubusercontent.com/95362045/170089633-d798519c-5339-4328-a4d7-9a29743f97e2.png)

Bom nesta área iremos primeiramente fazer um teste, vamos ver se conseguimos colocar duas vezes seguidas o mesmo cupom ? Iremos realizar o teste

![image](https://user-images.githubusercontent.com/95362045/170089857-b5e3718f-6a47-4069-b8d9-74c8897baa6c.png)

Ao aplicar duas vezes seguidas ele acusa que o cupom já está em uso, mas se tentarmos inserir intercalando ? Vamos testar.

![image](https://user-images.githubusercontent.com/95362045/170090038-ccad1279-218e-4118-977e-cf5d2014ef99.png)

Inserimos o cupom SINGUP30 e claramente foi aceito, vamos colocar novamente  NEWCUST5.

![image](https://user-images.githubusercontent.com/95362045/170090299-b275f1ce-0b0f-47cf-a309-b192c9585673.png)

Percebemos aqui que há uma regra de negocio, ele não aceita duas vezes o mesmo cupom iserindo uma atrás da outra porém não é tratado o fato que podemos colocar intercalando. Zeramos o preço do produto e agora é só finalizar a compra e finalizar a lab.

![image](https://user-images.githubusercontent.com/95362045/170090605-a633ecdd-fa59-403e-a099-0041316e3451.png)
