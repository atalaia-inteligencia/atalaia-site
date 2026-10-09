# Rollback do site

O ramo `main` publica sozinho no GitHub Pages, cerca de um minuto depois do push (cache de 10 minutos).
O repositório mora em `atalaia-inteligencia/atalaia-site` desde 18/09/2026.

## Versões

| Quando | Commit | Como era |
|---|---|---|
| 17/09/2026 | `346edac` | site original, guardado também em `index-antigo.html` |
| 17/09/2026 | `5b6d93b` | painel vivo com a cara do painel real (o que estava no ar antes da identidade Muralha) |
| 19/09/2026 | `27c025b` | identidade Muralha com a mesa de números; área do cliente escondida até a tela de login sair do nome do cliente |
| 21/09/2026 | `7192903` | só texto: o orçamento sai com o preço que a empresa definiu, pela IA ou pelo time (5 frases; antes dizia que preço, prazo e negociação ficavam com gente) |
| 28/09/2026 | `88347ee` | site novo: garantia de resposta, "Como funciona" com a cena Dois lados (anda com a rolagem), painel do time em HTML sem print, comparativo, preços, perguntas e o "em breve" dos ERPs |
| 29/09/2026 | `e1ece4e` | só texto: ajustes na IA inclusos na assinatura, em até 2 dias úteis (lista do que toda faixa inclui e uma pergunta do FAQ) |
| 29/09/2026 | `27355bb` | conserto: girar o tablet ou mudar a largura da janela não joga mais a página para o topo (só script, sem mudança visual) |
| 29/09/2026 | `ccaabbf` | conserto: a brasa da logo cresce redonda, sem o topo cortado reto (uma regra de CSS e um atributo nas 3 logos com brasa; nada muda de lugar) |
| 30/09/2026 | `110b24c` | tabela de preços nova: Entrada R$ 2.900, Crescimento R$ 5.500, Escala sob consulta, excedente R$ 3 (antes 1.500 / 2.500 / 4.500 / R$ 2) |
| 30/09/2026 | `4cf811f` | diagnóstico novo: até 8 perguntas com pulo e mini diagnóstico na tela; fim no WhatsApp |
| 30/09/2026 | `b42f7f0` | fechamento em duas portas: "A gente te procura" (formulário para o contato@, pelo serviço de contatos em api.atalaiainteligencia.com.br) ou WhatsApp |
| 02/10/2026 | `1be2483` | só texto: Crescimento até 2.500 conversas (antes 1.500), Escala "acima de 2.500 ou várias unidades" (antes "4.000, várias unidades") e a regra do excedente em 2.500; nenhum valor em reais mudou |
| 02/10/2026 | `bc42fde` | WhatsApp do site vai para o número comercial com IA de vendas (31) 9831-4312; frase "Nenhum cliente sem resposta. E a prova, em número."; linha "Para empresas que vendem pelo WhatsApp e têm um time atendendo."; "Do primeiro atendente ao time inteiro" no painel. Preço segue só na seção de preços. Voltar: `git revert` deste commit e dos 3 anteriores do PR #12 |
| 08/10/2026 | `6740816` | só texto: a demonstração do WhatsApp diz "cliente de uma empresa que vende peças" (antes "de uma distribuidora de peças"), para o site não repetir "distribuidora" do vídeo de lançamento. Voltar: `git checkout c38396e -- index.html` |
| 30/09/2026 | (este commit) | a área do cliente volta: botão "Área do cliente" no topo, bloco "Já é cliente" e link no rodapé, os três para `painel.atalaiainteligencia.com.br`, que passou a abrir o login da Atalaia (sem nome de cliente) |

## Voltar para antes da área do cliente (`0c9bf35`)

Só o `index.html` mudou (os 3 pontos perderam o `hidden` e saiu uma regra de CSS repetida). Para esconder de novo:

    git checkout 0c9bf35 -- index.html
    git commit -m "Rollback: esconde de novo a área do cliente"
    git push

Na fonte do site (`atalaia-site-fonte`, na máquina do Paulo) o mesmo efeito sai com `PORTAL = False` no
`build.py` e o build rodado de novo.

## Voltar para o fechamento só no WhatsApp (`4cf811f`)

Só o `index.html` mudou (o fim do diagnóstico e o texto de abertura da seção). Para desfazer:

    git checkout 4cf811f -- index.html
    git commit -m "Rollback: fim do diagnóstico volta a ser só WhatsApp"
    git push

Se o serviço de contatos cair, o formulário avisa "Não consegui enviar agora" e oferece o WhatsApp: não precisa de rollback só por isso.

## Voltar para os preços antigos (`ccaabbf`)

Só o `index.html` mudou (a seção de preços e a pergunta do excedente). Atenção: `ccaabbf` é de antes da área do
cliente, então este comando também a esconde. Para desfazer:

    git checkout ccaabbf -- index.html
    git commit -m "Rollback: volta a tabela de preços antiga"
    git push

## Voltar para a versão de 29/09, antes do conserto da brasa (`27355bb`)

Só o `index.html` mudou (a regra `svg:has(.atalaia-brasa)` e o `overflow="visible"` nas 3 logos). Para desfazer:

    git checkout 27355bb -- index.html
    git commit -m "Rollback: volta o site de antes do conserto da brasa"
    git push

## Voltar para a versão de 29/09, antes do conserto da rolagem (`e1ece4e`)

Só o `index.html` mudou (um trecho de script). Para desfazer:

    git checkout e1ece4e -- index.html
    git commit -m "Rollback: volta o site de antes do conserto da rolagem"
    git push

## Voltar para a versão de 28/09 (`88347ee`)

Só o `index.html` mudou (duas frases sobre os ajustes na IA). Para desfazer:

    git checkout 88347ee -- index.html
    git commit -m "Rollback: volta o site de 28/09"
    git push

## Voltar para a versão de 21/09 (`7192903`)

Só o `index.html` mudou (e este arquivo). A página nova não usa nenhum arquivo novo: fontes, favicons e `og.png` são os mesmos. Para desfazer:

    git checkout 7192903 -- index.html
    git commit -m "Rollback: volta o site de 21/09"
    git push

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
