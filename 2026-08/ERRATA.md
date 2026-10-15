# Versão 2026-08, erratas e mudança de esquema

O que se encontrou depois de a versão ter sido publicada, e como corrigir. Os ficheiros desta pasta não mudam; a correção faz-se ao lê-los.

## Esquema 2, desde a versão 2026-09

artigos.publicado_em nunca é posterior a artigos.recolhido_em. Quando o órgão declara uma data posterior à recolha, fica a da recolha, porque um artigo que o sítio já tinha lido estava publicado. Uma data sem fuso lê-se na hora de Lisboa; na versão 2026-08 foi lida como UTC, e as do Notícias ao Minuto têm lá uma hora a mais. historias.primeira_publicacao e historias.ultimo_artigo saem destas datas. A versão 2026-08 tem os dois erros, descritos abaixo. Uma data de meia-noite em ponto na hora de Lisboa, lida entre 3 e 24 horas depois, é um dia sem hora, e fica a da recolha. Em texto-partilhado, a terceira coluna é orgao, o identificador do órgão; na versão 2026-08 chamava-se artigo e trazia o número interno do órgão. artigos.seccoes passa a ter, num feed geral cujas etiquetas não nomeiam secção nenhuma, a secção que o endereço do artigo nomeia, exceto na RTP.

## Erratas

Errata de 25 de setembro de 2026. As datas de publicação de dois órgãos estão erradas nesta versão.

- Notícias ao Minuto. Nas 9 574 linhas do órgão em `artigos.csv.gz`, `publicado_em` tem uma hora a mais, porque o feed escreve a hora de Lisboa sem dizer o fuso e o sítio lia-a como UTC. Para corrigir, subtraia uma hora a `publicado_em` em todas as linhas do órgão.
- RTP. Em 3 277 das 3 738 linhas do órgão, `publicado_em` é posterior a `recolhido_em`, até 60 minutos. Para corrigir, use `recolhido_em` nessas linhas, e também em 4 linhas da Renascença e 1 do Público, adiantadas de segundos a oito minutos. As outras 461 linhas da RTP ficam como o feed as deu.
- Em `historias.csv.gz`, `primeira_publicacao` e `ultimo_artigo` saem destas datas e mudam em 8 316 das 25 103 histórias (a primeira em 7 572, a última em 7 174). Com a hora certa, as histórias 8882 e 8883 começam a 31 de julho, e as histórias 33969, 33992, 34018 e 34019 começam a 31 de agosto; estas quatro não estão nesta versão nem na de setembro.

Errata de 1 de outubro de 2026.

- Datas à meia-noite. Em 12 linhas de `artigos.csv.gz` (Diário dos Açores 10, CNN Portugal 1, Diário de Notícias 1), `publicado_em` é a meia-noite em ponto na hora de Lisboa e `recolhido_em` vem 3 a 24 horas depois, porque o órgão deu o dia sem a hora. Para corrigir, use `recolhido_em` nessas linhas. Em `historias.csv.gz`, `primeira_publicacao` muda em 12 histórias e `ultimo_artigo` em 10.
- `n_redacoes`. No `esquema.json` desta versão, a descrição diz que dois títulos do mesmo grupo contam como uma redação. Está errada; a propriedade não entra nesta conta. Os órgãos que publicaram o mesmo título ou o mesmo primeiro parágrafo com menos de 24 horas de intervalo contam como uma, e o número é o de grupos da história em `texto-partilhado.csv.gz`.
- `texto-partilhado.csv.gz`. A terceira coluna chama-se `artigo` e traz o número interno do órgão, e não o do artigo. Cada história tem uma linha por órgão, e um órgão que não partilhou texto com nenhum outro fica num grupo só seu. A partir da versão 2026-09, a coluna chama-se `orgao` e traz o identificador de `orgaos.orgao`. O órgão de cada número está na tabela seguinte.

| Número | orgao | Número | orgao | Número | orgao |
|---|---|---|---|---|---|
| 1 | publico | 22 | o-minho | 43 | mais-superior |
| 2 | observador | 23 | regiao-de-leiria | 44 | dnoticias-madeira |
| 3 | expresso | 24 | diario-as-beiras | 45 | acoriano-oriental |
| 4 | correio-da-manha | 25 | postal-do-algarve | 46 | correio-do-minho |
| 5 | diario-de-noticias | 26 | o-setubalense | 47 | diario-do-minho |
| 6 | jornal-de-noticias | 27 | noticias-de-viseu | 48 | diario-de-coimbra |
| 7 | nascer-do-sol | 28 | noticias-de-coimbra | 49 | diario-de-aveiro |
| 8 | sabado | 29 | a-voz-de-tras-os-montes | 50 | jornal-do-fundao |
| 9 | visao | 30 | medio-tejo | 51 | reconquista |
| 10 | noticias-ao-minuto | 31 | radio-campanario | 52 | mensageiro-de-braganca |
| 11 | 24noticias | 32 | funchal-noticias | 53 | diario-do-alentejo |
| 12 | rtp-noticias | 33 | diario-dos-acores | 54 | esquerda-net |
| 13 | sic-noticias | 34 | sul-informacao | 55 | avante |
| 14 | cnn-portugal | 35 | barlavento | 56 | povo-livre |
| 15 | tsf | 36 | diario-insular | 57 | o-diabo |
| 16 | renascenca | 37 | mensagem-de-lisboa | 454 | abrilabril |
| 17 | eco | 38 | o-corvo | 582 | tvi-noticias |
| 18 | jornal-de-negocios | 39 | fumaca | 804 | jornal-mapa |
| 19 | dinheiro-vivo | 40 | pagina-um | 805 | le-monde-diplomatique-pt |
| 20 | jornal-economico | 41 | gerador | 806 | shifter |
| 21 | lusa | 42 | setenta-e-quatro | | |
