# Rollback do site

O ramo `main` publica sozinho no GitHub Pages, cerca de um minuto depois do push (cache de 10 minutos).
O repositório mora em `atalaia-inteligencia/atalaia-site` desde 18/09/2026.

## Versões

| Quando | Commit | Como era |
|---|---|---|
| 17/09/2026 | `346edac` | site original, guardado também em `index-antigo.html` |
| 17/09/2026 | `5b6d93b` | painel vivo com a cara do painel real (o que estava no ar antes da identidade Muralha) |
| 19/09/2026 | `27c025b` | identidade Muralha com a mesa de números; área do cliente escondida até a tela de login sair do nome do cliente |
| 21/09/2026 | (este commit) | só texto: o orçamento sai com o preço que a empresa definiu, pela IA ou pelo time (5 frases; antes dizia que preço, prazo e negociação ficavam com gente) |

## Voltar para a versão de 19/09 (`27c025b`)

Só o `index.html` mudou depois dela (5 frases sobre preço). Para desfazer:

    git checkout 27c025b -- index.html
    git commit -m "Rollback: volta o texto de 19/09"
    git push

## Voltar para a versão anterior (`5b6d93b`)

Esta versão trocou a identidade visual inteira, então **não basta restaurar o `index.html`**: a página passou a
usar fontes, favicons, manifest e uma imagem de prévia de link (`og.png`) que a versão antiga não conhece.

    git checkout 5b6d93b -- index.html og.png
    git commit -m "Rollback: volta o site anterior à identidade Muralha"
    git push

O que sobra no repositório depois disso (`fontes/`, `favicon*`, `apple-touch-icon.png`, `icon-*.png`,
`site.webmanifest`) fica sem uso e não atrapalha: nenhuma página aponta para eles. Para limpar de vez:

    git rm -r fontes favicon.ico favicon.svg favicon-16.png favicon-32.png favicon-48.png \
      apple-touch-icon.png icon-192.png icon-512.png icon-maskable-512.png site.webmanifest

## Voltar para o site original (`346edac`)

Atenção: `og.png` **não existe** nesse commit (foi criado depois), então restaurá-lo junto faz o comando falhar.

    git checkout 346edac -- index.html
    git rm --cached og.png && rm og.png
    git commit -m "Rollback: volta o site original"
    git push

A segunda linha só é necessária se você quiser a página sem imagem de prévia, como ela era. Deixando o `og.png`
no lugar, o site antigo volta e a prévia de link continua com a marca nova, o que não quebra nada.

Sem git: copiar `index-antigo.html` por cima de `index.html`, commitar e dar push.

## Conferir depois do rollback

1. Abrir `https://atalaiainteligencia.com.br` numa janela anônima.
2. Conferir se o logotipo do topo é o esperado.
3. Testar a demonstração do WhatsApp e o diagnóstico de 4 perguntas (o botão tem que abrir o WhatsApp).
