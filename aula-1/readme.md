# Desafio

<center>

<h2>Eleições 2022 Fake</h2>
<img height='200' src='urna.jpg'/>
<p>Simulação do processo eleitoral</p>

</center>

## Diagrama

Desenahando a aplicação

![imagem](./1.jpg)
> https://app.diagrams.net/#G1WdhUMQIOzgTOYi27Qi4iM0g0yaj59XCA

- Envio das votações por tarefas
  - Utilizaremos a biblioteca node-bull com o provider Redis para enviar o voto
- Envio de e-mail confirmando o voto

## Requisitos
- Node JS
- Redis
- MySQL

## Links Úteis

- <https://app.diagrams.net/#G1WdhUMQIOzgTOYi27Qi4iM0g0yaj59XCA>
- <https://mailtrap.io/>
- <https://higher-order-programmer.medium.com/node-js-utilizando-filas-de-tarefas-ass%C3%ADncronas-com-bull-redis-71540f4be6ec>

```
Para usuários do DBeaver:

Clique com o botão direito na sua conexão, escolha "Editar Conexão"

Na tela "Configurações de conexão" (tela principal), clique em "Editar configurações do driver"

Clique em "Propriedades da conexão"

Clique com o botão direito na área "propriedades do usuário" e escolha "Adicionar nova propriedade"

Adicione duas propriedades: "useSSL" e "allowPublicKeyRetrieval"

Defina seus valores como "false" e "true" clicando duas vezes na coluna "value"

```