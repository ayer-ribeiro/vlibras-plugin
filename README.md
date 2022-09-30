# VLibras Widget

O VLibras Widget é um recurso de acessibilidade desenvolvido para tornar páginas web acessíveis para pessoas surdas. Com a tradução automática de Português Brasileiro para a Língua Brasileira de Sinais (LIBRAS), essa ferramenta permite que usuários surdos sejam capazes de consumir conteúdos de texto em qualquer website.

## Melhoria
A documentação oficial sugere que o código de integração seja adicionado antes do fechamento da tag <body>.
Isso é sugerido pela possibilidade de não funcionamento do código de integração causado pelo uso de 

```javascript
window.onload = ...
```
A alteração abaixo resolve faz com que o widget funcione de forma pouco mais robusta.

```diff
- var temp_f;\n\n\n    if(window.onload) {\n    \ttemp_f = window.onload;\n  \t}\n\n    window.onload = () => {\n\n\t  \tif(temp_f) {\n\t        temp_f();\n\t    }\n\n
+ document.addEventListener(\"DOMContentLoaded\", function() {
```

## Integrando a uma Página Web

```html
<body> <!-- Inicio do corpo da página -->

  ... <!-- Conteúdo da página -->


  <!-- Código de integração do VLibras Widget -->
  <div vw class="enabled">
    <div vw-access-button class="active"></div>
    <div vw-plugin-wrapper>
      <div class="vw-plugin-top-wrapper"></div>
    </div>
  </div>
  <script src="https://ayer-ribeiro.github.io/vlibras-plugin/vlibras-plugin.js"></script>
  <script>
    new window.VLibras.Widget('https://vlibras.gov.br/app');
  </script>
  <!-- Fim do código de integração com o VLibras -->
  
</body> <!-- Fim do corpo da página -->

Exemplo: https://github.com/ayer-ribeiro/vlibras-plugin/blob/main/demo/index.html
```
