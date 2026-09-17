# Rollback do site (17/09/2026)

O site anterior (commit 346edac) está guardado em `index-antigo.html`, com a pasta `prints/` que ele usa.

Para voltar ao site anterior em um comando (no PowerShell ou Git Bash, dentro deste repositório):

    git checkout 346edac -- index.html && git commit -m "Rollback: volta o site anterior" && git push

Ou, sem git: copiar `index-antigo.html` por cima de `index.html`, commitar e dar push. O GitHub Pages publica em cerca de um minuto (cache de 10 minutos).
