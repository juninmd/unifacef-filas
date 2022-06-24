# Aula 1

## Ementa
 - Apresentação
 - Requisitos
 - Desafio

---
## Apresentação

O que são serviços de mensageria?

# Requisitos
- NodeJS <https://nodejs.org/en/download/>
- Redis <https://www.docker.com/products/docker-desktop/> ou <https://medium.com/dockerbr/instalando-o-redis-em-um-container-docker-no-windows-a49b42988428>
- MySQL <https://www.docker.com/products/docker-desktop/> ou <https://dev.mysql.com/downloads/installer/>
- Postman <https://www.postman.com/downloads/>
- Redis Insight <https://redis.com/redis-enterprise/redis-insight/>
- Mailtrap <https://mailtrap.io/inboxes>
- Dbeaver <https://dbeaver.io/download/>

# Desafio

<center>

<h2>Eleições 2022 Fake</h2>
<img height='200' src='8.jpg'/>
<p>Simulação do processo eleitoral</p>

</center>

## Diagrama

Desenahando a aplicação

![imagem](./1.jpg)
> https://app.diagrams.net/#G1WdhUMQIOzgTOYi27Qi4iM0g0yaj59XCA

- Envio das votações por tarefas
  - Utilizaremos a biblioteca node-bull com o provider Redis para enviar o voto
- Envio de e-mail confirmando o voto
- Notificação via Web Socket para atualizar os votos em tempo real aos clientes web.

## Bull Dashboard
![imagem](./bull_dash.gif)

## Mail Trap
![imagem](./email.gif)

## Web Socket
![imagem](./votos.gif)

## Docker Desktop
> Containers Rodando

![imagem](./2.jpg)

> Container Redis com a connection sstring

![imagem](./3.jpg)

> Container MYSQL com a connection sstring

![imagem](./4.jpg)

> Página web simples <http://localhost:9001>

![imagem](./5.jpg)

## Dbeaver
> Devemos criar o database 'elections'

![imagem](./6.jpg)

```
Para usuários do DBeaver:
Clique com o botão direito na sua conexão, escolha "Editar Conexão"
Na tela "Configurações de conexão" (tela principal), clique em "Editar configurações do driver"
Clique em "Propriedades da conexão"
Clique com o botão direito na área "propriedades do usuário" e escolha "Adicionar nova propriedade"
Adicione duas propriedades: "useSSL" e "allowPublicKeyRetrieval"
Defina seus valores como "false" e "true" clicando duas vezes na coluna "value"
```

> Redis Insight

![imagem](./7.jpg)



## Links Úteis

- <https://app.diagrams.net/#G1WdhUMQIOzgTOYi27Qi4iM0g0yaj59XCA>
- <https://mailtrap.io/>
- <https://higher-order-programmer.medium.com/node-js-utilizando-filas-de-tarefas-ass%C3%ADncronas-com-bull-redis-71540f4be6ec>
- <https://www.blogdoft.com.br/2021/02/06/o-que-sao-mensageria-eventos-filas-e-topicos/>
- <https://www.youtube.com/watch?v=U5h6B7eSiAE>
- <https://www.youtube.com/watch?v=CYWEjcppJg0>
- <https://www.dinamize.com.br/blog/por-que-voce-deveria-utilizar-mensageria-na-aplicacao/>