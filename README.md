# MVP — Margem de projetos: o que explica as diferenças e onde proteger a margem

**Autora:** Marina del Giudice Chaves · **Disciplina:** PSP8 · **Professor:** André Luiz Marques Serrano · **Universidade de Brasília (UnB) — Engenharia de Produção**

## Objetivo
Construir um pipeline de dados em nuvem (arquitetura medalhão Bronze → Silver → Gold, modelo dimensional em esquema estrela) para responder:
**quais características dos projetos de 2026 (área, escopo, tipo de contrato, valor, prazo e composição da equipe) mais explicam as diferenças de margem
entre eles, e o que isso indica sobre quais projetos priorizar na originação e como alocar equipe para proteger a margem?**

Perguntas de apoio: (1) onde a margem se concentra? (2) a equipe explica a margem? (3) prazo e modelo de receita mexem na margem?

## Dados
Planilha gerencial *MVP Margem — Uso Público* de uma empresa de serviços profissionais organizada por projetos. Nomes de projetos e clientes foram substituídos por
rótulos e os valores em R$ foram descaracterizados. **A planilha original não está neste repositório** (uso restrito, autorização da empresa: ver `docs/`).

## Como reproduzir
1. Abra `notebooks/MVP_Margem_Pipeline_Medalhao.ipynb` no Google Colab.
2. Envie a planilha quando solicitado (ou coloque em `Meu Drive/MVP_Margem/entrada/`).
3. Execute todas as células. Tempo aproximado: 2 a 5 minutos.
4. As saídas ficam em `Meu Drive/MVP_Margem/` (bronze, silver, gold, catalogo, evidencias, relatorio, meta).

## Arquitetura
| Camada | Conteúdo | Formato |
|---|---|---|
| Bronze | cópia fiel em texto + metadados de ingestão (arquivo, aba, hash, data) | Parquet |
| Silver | tipagem, regras R00–R12 documentadas, margem recalculada de insumos primários, rateio de despesas indiretas | Parquet |
| Gold | dimensões (tempo, área, escopo, tipo, cargo, projeto), fatos (margem mensal, equipe mensal) e mart por projeto | Parquet + DuckDB com PK/FK |

Também são gerados o **Catálogo de Dados** (`catalogo/`), a **análise de qualidade** (verificações, tratamento e reavaliação) e a **linhagem** (`meta/`).

## Resultados
Resumo executivo, tabelas e gráficos em `relatorio/relatorio_mvp.html` e `relatorio/relatorio_mvp.md` (gerados pelo notebook).
<!-- Após executar, copie aqui os 3 principais achados e os links para as figuras em evidencias/. -->

## Limitações
Janela curta (mar–out/2026), regra de rateio de despesas indiretas que condiciona parte dos resultados, análise observacional (associação, não causalidade).
Detalhes na seção 12 do notebook.

## Checklist de entrega
- [ ] Objetivo e perguntas documentados
- [ ] Origem, licença e data de coleta registradas
- [ ] Dados persistidos na nuvem (Drive/DuckDB)
- [ ] Modelo de dados e Catálogo
- [ ] Transformação e carga documentadas
- [ ] Análise de qualidade cobrindo todos os atributos
- [ ] Respostas, evidências e discussão por pergunta
- [ ] Autoavaliação
- [ ] Capturas de tela da execução e do Drive em `evidencias/`
- [ ] Autorização da empresa registrada em `docs/`
- [ ] Repositório conferido em janela anônima, sem a planilha original

## Licença
Código sob MIT (ver `LICENSE`). Dados não distribuídos.
