# Doclytics — Landing page

Página de vendas do Doclytics, sistema de atribuição de receita por origem para clínicas.

## O que é

Site estático de arquivo único: `index.html`. Todo o CSS e o JavaScript estão embutidos
nele, e as únicas requisições externas são as fontes Inter e Inter Tight do Google Fonts.
Não há build, dependência ou servidor — abrir o arquivo no navegador já funciona.

## Publicar

Qualquer hospedagem de site estático serve. Na Vercel:

1. Importe este repositório em vercel.com
2. Não é preciso configurar build nem diretório de saída
3. Em *Settings → Domains*, aponte o domínio

## Limitação conhecida de SEO

Os guias existem para atrair busca orgânica, mas o arquivo único trabalha contra isso:
o Google recebe o mesmo HTML em `/guias/cac` e `/guias/roas`, e só vê o conteúdo certo
depois de executar o JavaScript. O roteador atualiza `<title>`, `meta description` e
`canonical` por rota para mitigar, mas indexação por renderização é mais lenta e há
risco de o Google tratar as URLs como duplicadas.

Se o tráfego orgânico não vier em três a quatro meses, separar cada guia em seu próprio
arquivo HTML resolve — é a mudança que mais aumenta a chance de ranquear.

## Pendências antes de ir ao ar

- [ ] O botão **Testar 3 dias grátis** aponta para `/cadastro`. Ajustar para a URL real
      do app caso ele fique em outro domínio ou subdomínio.
- [ ] Os links `/termos` e `/privacidade` no rodapé precisam existir no destino.
- [ ] A página não tem depoimentos nem números de clientes — incluir quando houver
      material real.

## Estrutura

```
index.html    o site inteiro (landing + termos + privacidade)
vercel.json   faz /termos e /privacidade servirem o index.html
README.md     este arquivo
.gitignore    proteção contra subir credenciais
```

**Tudo vive em um arquivo só.** As três páginas convivem no HTML como três blocos
`.view`, e um roteador de ~40 linhas mostra o que corresponde à URL. CSS e JavaScript
são embutidos; as únicas requisições externas são as fontes do Google Fonts.

## Como as rotas funcionam

| URL | O que aparece |
|---|---|
| `/` | landing page |
| `/termos` | Termos de Uso |
| `/privacidade` | Política de Privacidade |
| `/guias` | índice dos três guias |
| `/guias/cac` | guia de CAC |
| `/guias/roas` | guia de ROAS |
| `/guias/roi` | guia de ROI |

O `vercel.json` reescreve `/termos` e `/privacidade` para o `index.html`; o roteador lê
`location.pathname` e mostra o bloco certo. Clicar num link troca a view sem recarregar
a página, e o botão "voltar" do navegador funciona.

**Sem JavaScript, as três seções aparecem empilhadas** — feio, mas legível. Isso é
proposital: o conteúdo legal precisa estar acessível mesmo se o script falhar, e também
para robôs de busca.

Para testar localmente, use um servidor estático. Abrir o arquivo com dois cliques
(`file://`) funciona para ver a landing, mas as rotas `/termos` e `/privacidade` não,
porque o navegador as interpreta como pastas do disco.
