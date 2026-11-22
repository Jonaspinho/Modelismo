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

## Observações

- O `index.html` carrega `revistas.csv` com `fetch`. Se o navegador não conseguir ler o arquivo (por exemplo, ao abrir o `index.html` com duplo clique), a página usa uma cópia de reserva embutida no próprio HTML e avisa no menu lateral. Ao editar o CSV, atualize também essa cópia (bloco `csv-reserva`) se quiser que ela fique igual.
- PDFs hospedados no próprio repositório abrem no leitor sem problemas. Links de outros sites só abrem se o site permitir exibição em iframe; o botão **Abrir em nova aba** serve de alternativa.
- GitHub limita arquivos comuns a 100 MB.
- O botão **Carregar outro CSV** testa um arquivo local sem alterá-lo no repositório.
