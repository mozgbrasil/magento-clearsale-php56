![valid XHTML][checkmark]
[checkmark]: https://raw.githubusercontent.com/mozgbrasil/mozgbrasil.github.io/master/assets/images/logos/Red_star_32_32.png "MOZG"
[url-method]: http://portal.clearsale.com.br/solucoes/e-commerce/total
[requerimentos]: http://mozgbrasil.github.io/requerimentos/
[contact-clearsale]: http://portal.clearsale.com.br/solucoes/e-commerce/total
[tickets]: https://cerebrum.freshdesk.com/support/tickets/new
[preco]: http://www.cerebrum.com.br/preco/
[getcomposer]: https://getcomposer.org/
[uninstall-mods]: https://getcomposer.org/doc/03-cli.md#remove

# Mozg\ClearsaleTotal

## Sinopse

Integração a [Clearsale][url-method]

## Motivação

Atender o mercado de módulos para Magento oferecendo melhorias e um excelente suporte

## Suporte / Dúvidas

Para obter o devido suporte [Clique aqui][tickets], relatando o motivo da ocorrência o mais detalhado possível e anexe o print da tela para nosso entendimento

## Preço

[Clique aqui][preco]

## Recursos

Análise de registro

## Característica técnica

No frontend no /checkout/ é carregado o profiling onde é passado o session_id

No backend na grade de dados dos pedidos é possivel disparar analise em massa dos registros dos pedidos

No backend na visualização do pedido é possivel disparar analise do registro do pedido

## Instalação - Atualização - Desinstalação - Desativação

Este módulo destina-se a ser instalado usando o [Composer][getcomposer]

Antes de executar os processos, [clique aqui][requerimentos] e leia os pré-requisitos e sugestões

--

Certique se da existencia do arquivo composer.json na raiz do projeto Magento e que o mesmo tenha os trechos "minimum-stability", "prefer-stable", "repositories" e '"magento-root-dir":"./"', conforme https://gist.github.com/mozgbrasil/0c9bb8792ea6273ea24aed30b0fbcfba

Caso não exista o arquivo composer.json na raiz do projeto Magento, efetue o download

	wget https://gist.githubusercontent.com/mozgbrasil/0c9bb8792ea6273ea24aed30b0fbcfba/raw/9b514bc896171b6d75833b6f165065356f62ca59/composer.json

--

Para qualquer atualização no Magento sempre mantenha o Compiler e o Cache desativado

--

### Para instalar o módulo execute o comando a seguir no terminal do seu servidor

	composer require mozgbrasil/magento-clearsale-php56:dev-master

Você pode verificar se o módulo está instalado, indo ao backend em:

	STORES -> Configuration -> ADVANCED/Advanced -> Disable Modules Output

--

### Para atualizar o módulo execute o comando a seguir no terminal do seu servidor

	composer clear-cache && composer update

Na ocorrência de erro, renomeie a pasta /vendor/mozgbrasil e execute novamente

Para checar a data do módulo execute o seguinte comando

	grep -ri --include=*.json 'time": "' ./vendor/mozgbrasil

--

### Para [desinstalar][uninstall-mods] o módulo execute o comando a seguir no terminal do seu servidor

	composer remove mozgbrasil/magento-clearsale-php56 && composer clear-cache && composer update

--

### Para desativar o módulo

Renomeie a pasta do módulo

Cada módulo tem a sua pasta no diretório /vendor/mozgbrasil/

--

## Como configurar o método de antifraude

Para configurar o método de antifraude, acesse no backend em:

	∞ MOZG ∞ -> Anti-Fraud Methods ->  Total ClearSale, Total Guaranted & Application - (powered by MOZG)

Você terá os campos a seguir

### • **Ativar**

Para "ativar" ou "desativar" o uso do método

### • **Licença para uso comercial**

Informe a Licença para uso comercial

### • **Nome da ação**

Para ser exibido o debug do módulo informe na URL o seguinte parametro ?debug=true

Deve ser mapeado as UrlAction relativa

### • **Nome do bloco**

Para ser exibido o debug do módulo informe na URL o seguinte parametro ?debug=true

Deve ser mapeado o nome do bloco relativo

### • **Modo teste/produção**

Deve ser informado o devido ambiente

### • **Entity code - ambiente de teste**

Entity code relativo ao ambiente de teste

### • **Entity code - ambiente de produção**

Entity code relativo ao ambiente de produção

### • **FingerPrint App**

A ClearSale deverá informar qual valor deve ser utilizado. Essa informação serve para identificar o seu website no sistema da ClearSale.

### • **Tipo do e-commerce**

Tipo do e-commerce

### • **Relacionamento de pagamentos**

Informe a relação do seu método de pagamento ativo com o método de pagamento da ClearSale

## Perguntas mais frequentes "FAQ"

## Fluxo de integração

Este fluxo é responsável por demonstrar a integração entre o cliente e a ClearSale:

    Loja                                                                 ClearSale
     |                                                                       |
     |----- (A) solicitação de análise de risco (sendOrders) --------------->|
     |                                                                       | (B) realiza processamento
     |<---- (C) envia resposta ----------------------------------------------|
     |                                                                       |
     |----- (D) realiza a cobrança / cancela a compra / tenta novamente ---->|

* (A) A loja realiza uma solicitação de análise de risco, informando os dados da compra e do comprador.
* (B) A ClearSale processa a requisição.
* (C) A ClearSale responde a requisição.
* (D) Caso a resposta de (C) seja aprovada, a loja deverá realizar a cobrança.
* (D) Caso a resposta de (C) seja reprovada, a loja não deverá realizar a cobrança.
* (D) Caso a resposta de (C) seja aguardando aprovação, a loja deverá realizar novas consultas na plataforma na
ClearSale até que o status da análise mude para aprovado ou reprovado.

## Processo de Homologação

No Frontend, efetue a geração de 10 novos pedidos, na finalização de cada pedido efetue o logout da conta e repita novamente o processo de geração do novo pedido e nova conta.

Obs. No formulário de cadastro, caso o nosso módulo de clientes esteja ativo o mesmo tem automação de criação de conta ficticia para isso segure a tecla "Shift" em seguido de um "Duplo click" sobre o campo "Cidade", dessa forma deve ser auto-preenchido o formulário de cadastro com dados ficticios.

Se possível utilize o máximo de browsers simultâneo para agilizar o processo da criação dos pedidos.

Ao selecionar o(s) pedido(s) é possível disparar o processo para a "checagem de fraude"

Sendo exibido o retorno da ClearSale

Em seguida envie e-mail para "integracao@clearsale.com.br" e informe

	Boa Tarde

	Acabo de enviar 10 pedidos em massa para a ClearSale

	Favor efetuar homologação

	Fico no aguardo do EntityCode do ambiente de produção

	Conforme imagem vemos a integração do Fingerprint no /checkout/

	Os parâmetros "Prazo de Entrega" e "Dados do Cartão" devem ser enviado, caso tenha o registro armazenado

Caso não seja exibido o retorno da ClearSale, informe para que seja feita analise da ocorrência

O parâmetro "Fingerprint" deve ser enviado para todos os pedidos pois o script é integrado no /checkout/ se o mesmo não foi recebido é que pode ter ocorrido alguma instabilidade no serviço da ClearSale

O parâmetro "Prazo de Entrega" deve ser enviado, caso no método de entrega houver o registro do prazo  

Os parâmetros para "Dados do Cartão" deve ser enviado caso o método de pagamento armazene o número do cartão de crédito e suas demais informações no padrão da plataforma Magento como é o caso do método nativo "Cartão de crédito salvo", mas posso mapear atributos de módulos de terceiros

### Dados de contato - Clearsale

Para entrar em contato com a [Clearsale][contact-clearsale]

integracao@clearsale.com.br

Indira Marcela Borges O. dos Santos | Sustentação Técnica | Integração | +55 11 3728-8788 ramal 1332

## Manual

Total ClearSale, Total Guaranteed & Application - Versão 4.3

http://docdro.id/2lPwO0K

:cat2: