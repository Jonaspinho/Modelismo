# Catálogo de revistas de modelismo

Página estática com filtros (categoria, país, década), busca e leitor de PDF em tela cheia.

## Arquivos

- `index.html`: a página (HTML, CSS e JavaScript em um só arquivo)
- `revistas.csv`: os dados do catálogo (o `index.html` lê este arquivo ao abrir)
- `pdfs/`: coloque aqui os PDFs das revistas
- `capas/`: coloque aqui as imagens ou PDFs das capas

## Colunas do `revistas.csv`

| Coluna | Conteúdo |
| --- | --- |
| `titulo` | Título da revista (obrigatório) |
| `ano` | Ano de início |
| `pais` | País por extenso |
| `sigla` | Sigla do país (US, UK, DE, JP, BR...) |
| `categorias` | Uma ou mais, separadas por `;` (ex.: `Aeromodelismo;Militar`) |
| `data_publicacao` | Data da edição, no formato `AAAA-MM-DD` |
| `capa_url` | Link da capa, aberto em um iframe. Pode ficar vazio: a página gera uma capa de cor |
| `pdf_url` | Link do PDF, aberto no leitor |
| `download_url` | Link do botão **Baixar PDF** da tela de leitura. Se ficar vazio, o botão não aparece |

Para o download forçar o salvamento com o nome da revista, o arquivo precisa estar no mesmo site da página (por exemplo, `pdfs/arquivo.pdf` no GitHub Pages). Em links de outros sites o navegador pode apenas abrir o PDF em uma nova aba, e aí o usuário salva pelo próprio navegador.

Os links podem ser completos (`https://...`) ou caminhos do repositório (`pdfs/model-railroader-2026-10.pdf`, `capas/model-railroader.png`).
Se um campo tiver vírgula, coloque o valor entre aspas duplas.

## Publicar no GitHub Pages

1. Crie um repositório no GitHub e envie todos os arquivos desta pasta.
2. Em **Settings → Pages**, escolha **Deploy from a branch**, selecione a branch `main` e a pasta `/ (root)`.
3. Aguarde alguns minutos. O site fica em `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`.

Para testar no computador, não abra o `index.html` com duplo clique (o navegador bloqueia a leitura do CSV). Use um servidor local:

```
python3 -m http.server 8000
```

e acesse `http://localhost:8000`.

## De onde a página lê o CSV

No início do script do `index.html` existe a constante `CSV_URL`. Por padrão ela aponta para `revistas.csv` (mesmo repositório, no GitHub Pages). Para ler o CSV direto do GitHub, de qualquer página, troque por:

```
const CSV_URL="https://raw.githubusercontent.com/SEU-USUARIO/SEU-REPOSITORIO/main/revistas.csv";
```

- O repositório precisa ser público.
- Links do tipo `github.com/.../blob/...` também funcionam: a página converte para o endereço raw.
- Para testar outro CSV sem mexer no código: `https://SEU-SITE/?csv=ENDERECO-DO-CSV`.
- Depois de editar o CSV no GitHub (botão de lápis, ou novo commit), basta recarregar a página. O endereço raw pode demorar alguns minutos para refletir a mudança por causa do cache do GitHub.
- Links relativos de `pdf_url` e `capa_url` (como `pdfs/arquivo.pdf`) são resolvidos a partir do endereço da página, então funcionam quando os PDFs estão no mesmo site do GitHub Pages. Se a página estiver em outro lugar, use links completos.

## Observações

- O catálogo carrega conforme a rolagem: 12 revistas por vez, e mais 12 a cada vez que o fim da lista se aproxima. O tamanho do bloco está na constante `PAGE`, no `index.html`.
- PDFs hospedados no próprio repositório abrem no leitor sem problemas. Links de outros sites só abrem se o site permitir exibição em iframe; o botão **Abrir em nova aba** serve de alternativa.
- GitHub limita arquivos comuns a 100 MB.
- O botão **Carregar outro CSV** testa um arquivo local sem alterá-lo no repositório.
