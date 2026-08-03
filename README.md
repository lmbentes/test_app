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

A app consegue fotografar a etiqueta de um frasco e preencher automaticamente os campos Frasco, Nº, Destino e Nº Amostra:

- **Sem chave API**: usa OCR local e gratuito (Tesseract.js), que corre no telemóvel. Precisa de internet só na primeira leitura (para descarregar o modelo de português), depois funciona sem custos.
- **Com chave API da Anthropic**: leitura mais robusta feita por IA, indicada para etiquetas com letra manuscrita ou mais confusas.

Para configurar a chave (opcional):
1. Cria uma conta em [console.anthropic.com](https://console.anthropic.com).
2. Vai a **API Keys** e cria uma chave nova.
3. Na app, abre **Definições** e cola a chave.
4. A chave fica guardada só no teu telemóvel.

**Nota sobre custos:** só a opção com chave API consome créditos da tua conta Anthropic (uma fração de cêntimo por leitura). A opção sem chave (Tesseract) é sempre grátis.

## Gerar um relatório em Excel (conversor-relatorio.html)

O ficheiro `conversor-relatorio.html` (incluído nesta pasta) é uma ferramenta separada, para usar no teu computador — não precisa de estar no GitHub Pages nem de internet depois de aberta uma vez.

1. Na app, vai a **Definições → Guardar cópia** e exporta o `.json` (por exemplo, para o Google Drive) e depois transfere-o para o PC.
2. Abre o ficheiro `conversor-relatorio.html` diretamente no browser do PC (basta clicar duas vezes).
3. Escolhe o ficheiro `.json` (ou vários, se tiveres mais do que um) e toca em **"Gerar Excel"**.
4. É descarregado um `.xlsx` com três folhas: **Locais** (um por linha, com maré, GPS, parâmetros de campo, etc.), **Frascos** (um por linha, com Frasco/Nº/Destino/Nº Amostra/Recolhido) e **Resumo por Destino** (totais).

Como cada cópia exportada da app já contém todo o histórico guardado no telemóvel, normalmente basta usares sempre o ficheiro mais recente — só precisas de juntar vários ficheiros no conversor se tiveres apagado dados entretanto e quiseres recuperar colheitas antigas.

Este Excel gerado é, na prática, a tua "base de dados" — mantém-no e volta a gerá-lo (substituindo o anterior) sempre que quiseres atualizar o relatório com as colheitas mais recentes.

## Notas técnicas

- Dados guardados em `localStorage` do Safari. Se limpares os dados do site no iPhone (ou desinstalares a app do ecrã principal e limpares o Safari), perdes o histórico — não há backup automático.
- O `sw.js` (service worker) permite que a app abra mesmo sem rede depois da primeira visita, mas a leitura automática de etiquetas precisa sempre de internet.
- Sem build step: é HTML/CSS/JS puro, não precisa de `npm install` nem de servidor — basta servir os ficheiros estáticos (é para isso que serve o GitHub Pages).
