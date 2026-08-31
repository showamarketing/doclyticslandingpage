# DocLytics — Landing page

Página de vendas do DocLytics, sistema de atribuição de receita por origem para clínicas.

## O que é

Site estático de arquivo único: `index.html`. Todo o CSS e o JavaScript estão embutidos
nele, e as únicas requisições externas são as fontes Inter e Inter Tight do Google Fonts.
Não há build, dependência ou servidor — abrir o arquivo no navegador já funciona.

## Publicar

Qualquer hospedagem de site estático serve. Na Vercel:

1. Importe este repositório em vercel.com
2. Não é preciso configurar build nem diretório de saída
3. Em *Settings → Domains*, aponte o domínio

## Pendências antes de ir ao ar

- [ ] O botão **Testar 3 dias grátis** aponta para `/cadastro`. Ajustar para a URL real
      do app caso ele fique em outro domínio ou subdomínio.
- [ ] Os links `/termos` e `/privacidade` no rodapé precisam existir no destino.
- [ ] A página não tem depoimentos nem números de clientes — incluir quando houver
      material real.

## Estrutura

```
index.html    página completa (HTML + CSS + JS embutidos)
README.md     este arquivo
.gitignore    proteção contra subir credenciais
```
