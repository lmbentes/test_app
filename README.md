# Colheita de Água

Webapp simples para preparar e controlar colheitas de água: registo de local, maré, foto, posição GPS, e uma tabela de frascos (Frasco / Nº / Destino / Nº Amostra) com leitura automática das etiquetas por foto.

Todos os dados ficam guardados **apenas no teu telemóvel** (não há servidor nem base de dados — funciona 100% no browser).

## Colocar no GitHub Pages

1. Cria um repositório novo no GitHub (pode ser privado ou público).
2. Faz upload de todos os ficheiros desta pasta para a raiz do repositório:
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `icon-192.png`
   - `icon-512.png`
3. Vai a **Settings → Pages** no repositório.
4. Em "Source", escolhe a branch `main` e a pasta `/ (root)`. Guarda.
5. Ao fim de 1–2 minutos o GitHub dá-te um link do género:
   `https://<o-teu-utilizador>.github.io/<nome-do-repositorio>/`

## Instalar no iPhone (ecrã principal)

1. Abre o link acima no **Safari** do iPhone (tem de ser o Safari, não o Chrome, para o "Adicionar ao ecrã principal" funcionar bem).
2. Toca no ícone de **Partilhar** (o quadrado com a seta a apontar para cima).
3. Escolhe **"Adicionar ao Ecrã Principal"**.
4. Confirma o nome e toca em **"Adicionar"**.

A partir daí abre como uma app normal, em ecrã inteiro, com ícone próprio.

Na primeira vez que usares a câmara e o GPS, o iPhone vai pedir permissão — tens de aceitar para essas funções funcionarem.

## Ativar a leitura automática das etiquetas (opcional)

A app consegue fotografar a etiqueta de um frasco e preencher automaticamente os campos Frasco, Nº, Destino e Nº Amostra, usando a API da Anthropic (Claude). Fora do ambiente do Claude.ai, isto precisa de uma chave API tua:

1. Cria uma conta em [console.anthropic.com](https://console.anthropic.com).
2. Vai a **API Keys** e cria uma chave nova.
3. Na app, abre **Definições** (no fundo do ecrã principal) e cola a chave.
4. A chave fica guardada só no teu telemóvel (localStorage do Safari) — nunca é enviada para mais lado nenhum.

Sem chave configurada, a app continua a funcionar normalmente — só a leitura automática fica desativada, e preenches a tabela à mão (com sugestões automáticas de número, destino, etc.).

**Nota sobre custos:** cada leitura de etiqueta consome créditos da tua conta Anthropic (é uma chamada à API com imagem). Consulta os preços atuais em anthropic.com — para o volume normal de uma colheita de campo, o custo é tipicamente uma fração de cêntimo por leitura.

## Notas técnicas

- Dados guardados em `localStorage` do Safari. Se limpares os dados do site no iPhone (ou desinstalares a app do ecrã principal e limpares o Safari), perdes o histórico — não há backup automático.
- O `sw.js` (service worker) permite que a app abra mesmo sem rede depois da primeira visita, mas a leitura automática de etiquetas precisa sempre de internet.
- Sem build step: é HTML/CSS/JS puro, não precisa de `npm install` nem de servidor — basta servir os ficheiros estáticos (é para isso que serve o GitHub Pages).
