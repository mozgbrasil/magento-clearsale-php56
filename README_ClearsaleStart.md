[checkmark]: https://raw.githubusercontent.com/mozgbrasil/mozgbrasil.github.io/master/assets/images/logos/logo_32_32.png "MOZG"
![valid XHTML][checkmark]

[url-method]: http://portal.clearsale.com.br/solucoes/e-commerce/start
[requerimentos]: http://mozgbrasil.github.io/requerimentos/
[contact-clearsale]: http://portal.clearsale.com.br/solucoes/e-commerce/start
[tickets]: https://cerebrum.freshdesk.com/support/tickets/new
[preco]: http://www.cerebrum.com.br/preco/
[getcomposer]: https://getcomposer.org/
[uninstall-mods]: https://getcomposer.org/doc/03-cli.md#remove
[artigo-composer]: http://mozg.com.br/ubuntu/composer
[ioncube-loader]: http://www.ioncube.com/loaders.php
[acordo]: http://mozg.com.br/acordo-licenca-usuario-final/

# Mozg\ClearsaleStart

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

No backend na grade de dados dos pedidos é possivel disparar analise em massa dos registros dos pedidos

No backend na visualização do pedido é possivel disparar analise do registro do pedido

## Instalação - Atualização - Desinstalação - Desativação

--

Este módulo destina-se a ser instalado usando o [Composer][getcomposer]

Execute o seguinte comando no terminal, para visualizar a existencia do Composer e sua versão

	composer --version

Caso não tenha o Composer em seu ambiente, sugiro ler o seguinte artigo [Clique aqui][artigo-composer]

--

É necessário que o servidor tenha o suporte a extensão [ionCube PHP Loader][ioncube-loader]

Para visualizar se essa extensão está ativa em seu servidor

Certique se da presença do arquivo phpinfo.php na raiz do seu projeto

	<?php phpinfo(); ?>

Caso não exista o arquivo phpinfo.php na raiz do projeto Magento, crie o mesmo adicionado o conteúdo acima

Acesse o arquivo pelo browser

Em seguida pesquise pelo termo "ionCube PHP Loader"

Caso o seu servidor não tenha o suporte a extensão, [Clique aqui][ioncube-loader]

Em "Loader Downloads API", efetue download do pacote compatível com o seu servidor

Descompacte o pacote e faça upload do arquivo "loader-wizard.php" para seu servidor, onde será demonstrado o passo a passo para a ativação da extensão

[Clique aqui](https://youtu.be/GZ2J6MLkko4) para ver os processos executados

--

Para utilizar o(s) módulo(s) da MOZG é necessário aceitar o [Acordo de licença do usuário final][acordo]

--

Sugiro manter um ambiente de testes para efeito de testes e somente após os devidos testes aplicar os devidos procedimento no ambiente de produção

--

Sugiro efetuar backup da plataforma Magento e do banco de dados

--

Antes de efetuar qualquer atualização no Magento sempre mantenha o Compiler e o Cache desativado

--

Certique se da presença do arquivo composer.json na raiz do seu projeto Magento e que o mesmo tenha os parâmetros semelhantes ao modelo JSON abaixo

	{
	  "minimum-stability": "dev",
	  "prefer-stable": true,
	  "license": [
	    "proprietary"
	  ],
	  "repositories": [
	    {
	      "type": "composer",
	      "url": "https?://packages.firegento.com"
	    }
	  ],
	  "extra": {
	    "magento-root-dir": "./",
	    "magento-deploystrategy": "copy",
	    "magento-force": true
	  }
	}

Caso não exista o arquivo composer.json na raiz do projeto Magento, crie o mesmo adicionado o conteúdo acima

### Para instalar o módulo execute o comando a seguir no terminal do seu servidor no diretório do seu projeto

	composer require mozgbrasil/magento-clearsale-php56:dev-master

Você pode verificar se o módulo está instalado, indo ao backend em:

	STORES -> Configuration -> ADVANCED/Advanced -> Disable Modules Output

--

### Para atualizar o módulo execute o comando a seguir no terminal do seu servidor no diretório do seu projeto

Antes de efetuar qualquer processo que envolva atualização no Magento é recomendado manter o Compiler e Cache desativado

	composer clear-cache && composer update

Na ocorrência de erro, renomeie a pasta /vendor/mozgbrasil e execute novamente

Para checar a data do módulo execute o seguinte comando

	grep -ri --include=*.json 'time": "' ./vendor/mozgbrasil

--

### Para [desinstalar][uninstall-mods] o módulo execute o comando a seguir no terminal do seu servidor no diretório do seu projeto

	composer remove mozgbrasil/magento-clearsale-php56 && composer clear-cache && composer update

--

### Para desativar o módulo

1. Antes de efetuar qualquer processo que envolva atualização sobre o Magento é necessário manter o Compiler e Cache desativado

2. Caso queira desativar os módulos da MOZG renomeie a seguinte pasta app/code/local/Mozg

A desativação do módulo pode ser usado para detectar se determinada ocorrência tem relação com o módulo

--

## Como configurar o método de antifraude

Para configurar o método de antifraude, acesse no backend em:

	∞ MOZG ∞ -> Anti-Fraud Methods ->  ClearSale Start - (powered by MOZG)

Você terá os campos a seguir

### • **Ativar**

Para "ativar" ou "desativar" o uso do método

### • **Licença para uso comercial**

Informe a Licença para uso comercial

### • **Modo teste/produção**

Deve ser informado o devido ambiente

### • **Entity code - ambiente de teste**

Entity code relativo ao ambiente de teste

### • **Entity code - ambiente de produção**

Entity code relativo ao ambiente de produção

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

### Dados de contato - Clearsale

Para entrar em contato com a [Clearsale][contact-clearsale]

Sustentação Técnica (Problemas Técnicos): 11 3728-8788

Suporte: suporte@clearsale.com.br

## Manual

ClearSale Start - Versão 2.0

http://docdro.id/7B1jKsy

:cat2:
