---
layout: post
title:  "Testando o seu CSS"
date:   2015-02-08 14:34:25
categories: css
tags: 
image: /assets/article_images/2015-02-08-alterando-a-cor-da-barra-de-navegacao/534421887_e17afcac3a_o.jpg
---
O que? Testar o CSS? Como? Calma é isso mesmo não é nunhuma coisa de outro mundo, e eu vou lhe mostrar como realizar estes testes.

# Tipos de teste
- Sintaxe
- Padrões de Projeto
- Referência / Regressão

Neste post irei explicar o é e como realizar testes de Referência / Regressão.

Teste de regressão

# Porquê?
CSS é uma linguagem fácil então é fácil fazer qualquer alteração e com isso também é muito fácil quebrar alguma coisa. E como você faz para testar todas as alterações que foram feitas? Abre todas as páginas do site/sistema manualmente em todos os navegadores para ver se esta tudo OK? Abre só no navegador que você utiliza para o desenvolvimento, checa nele e confia no seu taco?
Nenhuma destas opções são muito eficientes. No primeiro caso você ou alguem do time irá perder muito tempo para ficar verificando todo o site em busca de alguma parte que está quebrada. E no segundo cenário você acaba testando apenas em um navegador e deixando para testar nos outros quando subir para produção.

> O teste de regressão é uma técnica do teste de software que consiste na aplicação de versões mais recente do software, para garantir que não surgiram novos defeitos em componentes já analisados. Se, ao juntar o novo componente ou as suas alterações com os componentes restantes do sistema surgirem novos defeitos em componentes inalterados, então considera-se que o sistema regrediu.

http://pt.wikipedia.org/wiki/Teste_de_regress%C3%A3o

# Como?
Basicamente a ferramenta que eu irie mostrar e todas as outras gravam um screenshot da tela / bloco em uma versão base, que seria a versão onde está tudo OK e a depois seriam gravados outros screenshots com as alterações realizadas e comparado com a versão base previamente salva.

# Ferramentas
Atualmente existem várias bibliotecas que realizam teste de regressão, quando comecei a estudar sobre o assunto comecei a ver tantas bibliotecas diferentes que não sabia qual utilizar, como disse anteriormente todas funcionam do mesmo jeito a única diferença é o suporte à navegadores que cada uma oferece. Algumas oferecem apenas suporte ao Phantomjs (webkit), outras ao CasperJS(webkit/gecko) e algumas ao Selenium, Saucelabs e BrowserStack.

- [BackstopJS][BackstopJS] (PhantomJS)
- [Viff][viff] (Selenium)
- [pix-diff][pix-diff] (Protractor, Selenium)
- [Applittools][applittools] (PhantomJS)
- [PhantomCSS][PhantomCSS] (PhantomJS)
- [wraith][wraith] (PhantomJS, SlimerJS)
- [webdrivercss][webdrivercss] (Selenium)

# Me mostre como
Neste artigo irei mostrar como utilizar o [wraith][wraith] que foi criado pelo BBC, com ele você poderá executar os testes utilizando o PhantomJS (webkit) e o SlimerJS (Gecko).

## Instalando
Todas as dependências e estão listadas [neste link][wraith-install].
Após instalar todas as dependências necessárias, você deve instalar o wraith.
{% highlight ruby %}
gem install wraith
{% endhighlight %}

## Criando um projeto
Para criar um projeto com do wraith você deverá criar uma pasta. Após criar a pasta você deverá iniciar o projeto com o seguinte comando:
{% highlight ruby %}
wraith setup
{% endhighlight %}

Este comando irá a seguinte estrutura de pasta:
{% highlight shell %}
.
├── configs
│   └── config.yaml
└── javascript
    └── snap.js
{% endhighlight %}

## Configurando o projeto
Todas as configurações necessárias serão feitas no arquivo configs/config.yaml, abaixo irei explicar as opções existentes.

*browser*
está opção indica qual será o navegador utilizado nos testes, as opções disponíveis são phantomjs e slimerjs. É possível utilizar os dois navegadores.
{% highlight ruby %}
browser:
  phantomjs: "phantomjs"
  slimerjs: "slimerjs"
{% endhighlight %}

*snap_file*

*directory*
diretório onde serão salvos os screenshots

*domains*
domínios que serão utilizados nos testes, deve ser informado apenas 2 domínios.

*screen_widths*
lista dos tamanhos de tela (largura).

*paths*
caminhos que serão testados, baseados nos *domains* informados

*fuzz*

*spider_days*

*mode*
como os resultados serão exibidos, por padrão é exibido em ordem alfabética. As opções disponíveis são:
- alphanumeric, que é a opção padrão
- diffs_first, ira ser exibido primeiro os caminhos que possuem diferença
- diffs_only, ira ser exibido apenas os caminhos que possuem diferença

*threshold*


[BackstopJS]: https://garris.github.io/BackstopJS/
[viff]: https://github.com/winsonwq/viff
[pix-diff]: https://github.com/koola/pix-diff
[applittools]: https://applitools.com/
[PhantomCSS]: https://github.com/Huddle/PhantomCSS
[wraith]: https://github.com/BBC-News/wraith
[webdrivercss]: https://github.com/webdriverio/webdrivercss
[wraith-install]: http://bbc-news.github.io/wraith/os-install.html
