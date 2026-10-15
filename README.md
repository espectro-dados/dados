# dados

O registo do espectro, oespectro.eu, em ficheiros mensais. O espectro lê os feeds de 62 órgãos de informação portugueses, junta numa história os artigos sobre o mesmo acontecimento e guarda quem publicou o quê e quando, desde 7 de agosto de 2026. Mantém também o registo dos órgãos, com o dono de cada título e as fontes dessa leitura. Este repositório tem tudo isso em CSV, uma pasta por mês, para quem queira contar, conferir ou estudar.

![Artigos por grupo proprietário, setembro de 2026](https://oespectro.eu/medicoes/2026-09/grafico/donos.png)

## Ficheiros de cada versão

| Ficheiro | Conteúdo |
|---|---|
| `orgaos.csv.gz` | Os órgãos do registo no dia em que a versão foi gerada, com o dono de cada um. |
| `donos.csv.gz` | Os proprietários e os títulos que detêm. |
| `historico-propriedade.csv.gz` | Cada leitura registada da propriedade de um órgão, com a data. |
| `feeds.csv.gz` | As fontes lidas em cada órgão e o estado da leitura. |
| `historias.csv.gz` | As histórias com primeiro artigo no mês, com datas e contagens de artigos, órgãos e redações. |
| `artigos.csv.gz` | Os artigos recolhidos no mês, com órgão, história, datas, endereço, secções e países. |
| `texto-partilhado.csv.gz` | Os órgãos de cada história agrupados pelo texto que partilharam. |
| `versoes-de-titulo.csv.gz` | Cada troca de título de um artigo, quando e por que ordem, sem o texto. |
| `esquema.json` | As colunas de cada tabela, com tipo e descrição. |
| `manifest.json` | Bytes, linhas e SHA-256 de cada ficheiro, o período e a data de geração. |
| `SHA256SUMS` | As mesmas somas, para `sha256sum -c SHA256SUMS`. |

CSV em UTF-8 sem BOM, comprimido com gzip. Instantes em ISO 8601, UTC. Listas separadas por `|`. A descrição de cada coluna está no `esquema.json` da versão e em https://oespectro.eu/dados#tabelas.

## Ler uma versão

```python
import pandas as pd

artigos = pd.read_csv("2026-09/artigos.csv.gz")
orgaos = pd.read_csv("2026-09/orgaos.csv.gz")
por_dono = artigos.merge(orgaos[["orgao", "dono"]], on="orgao").groupby("dono").size()
print(por_dono.sort_values(ascending=False).head(10))
```

Antes de ler, `sha256sum -c SHA256SUMS` dentro da pasta da versão confere os ficheiros.

## O que não está aqui

Os títulos e os textos dos artigos pertencem aos órgãos que os publicaram e não se distribuem em bloco. Os ficheiros trazem os endereços; o texto lê-se na fonte. Também não estão as posições editoriais, que só se mostram no sítio ao lado das fontes que as sustentam.

## Versões

| Versão | Período | Gerada a | Esquema | Notas |
|---|---|---|---|---|
| `2026-08` | 7 a 31 de agosto de 2026 | 24 de setembro de 2026 | 1 | [erratas](2026-08/ERRATA.md) |
| `2026-09` | 1 a 30 de setembro de 2026 | 2 de outubro de 2026 | 2 | |

Uma versão fecha depois de o mês acabar e os ficheiros não voltam a mudar. Um erro encontrado depois fica numa errata, na pasta da versão, com a forma de o corrigir. A versão seguinte sai no dia 2 de cada mês.

## Licença e citação

CC BY 4.0, texto integral em `LICENSE`. Cite a versão e não o repositório, por exemplo «espectro, oespectro.eu/dados/2026-09, gerada a 2 de outubro de 2026». O `CITATION.cff` tem a citação da versão mais recente.

## Contacto

contacto@oespectro.eu, para erros e para campos que faltem. Um campo pedido por um projeto com nome entra na versão seguinte.
