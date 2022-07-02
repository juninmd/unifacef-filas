# RabbitMQ

# AMQP
É um protocolo que “roda acima” do protocolo TCP, que pertence à camada de transporte. É um protocolo que permite o envio e recebimento de mensagens de forma assíncrona – ou seja, quando enviamos uma mensagem não esperamos uma resposta imediata – independente do hardware, sistema operacional e linguagem de programação. 


## Sobre o RabbitMQ

O RabbitMQ é um software de mensagens com código aberto, que implementou o protocolo "Advanced Message Queuing Protocol"


Binding: É a ligação entre uma fila e um exchange
Binding key: É uma chave específica da ligação entre a fila e o exchange
Routing key: É uma chave enviada junto a mensagem que o exchange usa para decidir para que fila (ou filas) vai rotear uma mensagem.

Exchanges
Se você não sabe o são exchanges entre aqui e descubra. Mas, basicamente eles são os elementos da arquitetura do protocolo AMQP que recebem as mensagens e as encaminham para filas de acordo com os bindings e o tipo declarado da exchange.

Assim como filas e mensagens as exchanges também podem ser duráveis, ou seja, são recriadas caso o servidor caia por algum motivo.

Mais detalhes sobre o que são todos os itens que citei estão, ou deveriam estar, no link acima.

Tipos de exchange
O protocolo AMQP na versão 0-9-1 fornece cinco tipos de exchange:

Default exchange;
Direct exchange;
Fanout exchange;
Topic exchange;
Headers exchange;
Falarei delas abaixo.

Default exchange
Esse é o exchange padrão fornecida pelo broker e, não possui nome. Apesar disso, tem uma característica muito interessante: toda fila criada é automaticamente associada a ela com uma rota que é igual ao nome da fila. Em miúdos, se eu declarar uma fila com o nome foo e publicar uma mensagem no default exchange com a rota foo esta mensagem será entregue na fila de mesmo nome, dando a impressão que estou me comunicando diretamente com a fila.

Importante: Eu acho muito fácil confundir este exchange com o próximo por causa do seu comportamento. A impressão de estar se comunicando direto com a fila nos leva a crer que estamos lidando com um exchange do tipo direct. É muito importante ressaltar que não é isso que acontece! As mensagens em nenhum momento são entregues diretamente nas filas (sem passar antes pelo exchange)!

Direct exchange
Diferente do exchange apresentado anteriormente, este possui nome e seu comportamento é de encaminhar mensagens que possuam exatamente a mesma rota das filas associadas a este exchange.

Exemplificando:

Uma fila se associa a um exchange com a rota foo. Quando uma nova mensagem com a rota foo chega no direct exchange ele a encaminha para a fila foo.

O direct exchange é uma ótima opção para trabalhar com diversos consumers de maneira balanceada já que o algoritmo utilizado pelo RabbitMQ para distribuição de mensagens entre consumers é o round-robin.

Fanout exchange
Este exchange simplesmente ignora a rota. Seu comportamento resume-se em mandar uma cópia das mensagens para todas as filas que estão associadas a ele.

Um bom exemplo de uso para este tipo de exchange é fazer o broadcast de uma mudança de configuração para n filas, fazendo com que seus respectivos consumers repliquem as alterações.

Topic exchange
Este exchange encaminha mensagens de acordo com a rota definida na mensagem e o padrão definido na associacão da fila ao exchange. Por exemplo, vamos supor que eu queira agregar logs do Apache. Eu defini que vou ter filas distintas para acesso e erros e uma fila que vai receber os dois tipos.

Os bindings seriam os seguintes:

Q1 (logs de acesso): apache.access;
Q2 (logs de erro): apache.error;
Q3 (logs de erro): apache.*;
Então, se meu producer mandar uma mensagem com rota apache.access tanto a fila Q1 quanto a fila Q3 receberão as mensagens porque o padrão (como se fosse uma regex) bate. O mesmo vale se meu producer enviar uma mensagem com a rota apache.error, a diferença é que a fila Q2 receberá mensagem ao invés da fila Q1.

É muito importante ressaltar que os padrões tem duas regras básicas o * substitui apenas UMA palavra. Se você quiser substituir zero ou mais (assim como o operador * da regex) você precisa usar o #.

Headers exchange
Esse é o tipo menos comum de exchange. Este tipo ignora a rota e encaminha as mensagens usando seu cabeçalho. Então se você possui uma condição mais complexa que uma string para encaminhar a mensagem você pode fazer uso deste tipo de exchange. Ele funciona BEM mais ou menos como um if, já que é possível definir mais de um critério para encaminhamento da mensagem, e ainda possibilita o uso de hashes ou inteiros como “rotas” se houver a necessidade de usar algo mais complexo.

Conclusão
Se o sistema que você deseja utilizar o RabbitMQ for simples é possível que você apenas use o default exchange, vá criando filas conforme sua necessidade e vá produzindo mensagens de acordo com a fila que deseja utilizar, uma máquina de estados pode muito bem funcionar dessa forma, por exemplo.

Caso seu sistema precise distribuir mensagens entre diversos consumers o direct exchange é o ideal para você já que apenas mensagens com rotas específicas serão distribuídas.

Se você precisa que as mensagens produzidas sejam replicadas para mais de uma fila, o fanout exchange pode fazer isso para você.

Se o seu caso for o de precisar um pouco mais de flexibilidade para o encaminhamento das mensagens, o topic exchange possibilita a construção de padrões de rota.

E, finalmente se você precisa de condições mais complexas que as citadas acima ou não quer/pode usar uma string como rota, o headers exchange supre a sua necessidade.

Apesar, da complexidade aparente dos exchanges não é preciso conhecer e muito menos usar todos em sua aplicação, escolha um que satisfaça sua necessidade e planeje muito bem sua arquitetura para que seja possível mudar algo se for necessário com o mínimo de impacto possível.

