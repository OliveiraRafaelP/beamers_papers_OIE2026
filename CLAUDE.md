# Papers OI — Contexto do Projeto

**Curso:** Organização Industrial Empírica (ouvinte)
**Programa:** Doutorado — Faculdade de Economia, Administração e Contabilidade (FEA-USP)
**Período:** 2026, Primeiro Semestre, Primeiro Bimestre
**Responsável:** Rafael Pereira Oliveira

Esta pasta contém os artigos acadêmicos mais relevantes apresentados na disciplina, cada um em sua própria subpasta numerada. Para cada artigo foram gerados: (1) um resumo didático em Word (.docx) e (2) um código LaTeX Beamer de apresentação (.txt). Os papers foram processados por dois pipelines distintos, descritos abaixo.

O arquivo `lista_papers_OIE.xlsx` (raiz desta pasta) contém a lista completa dos 42 artigos planejados para a disciplina, incluindo status de processamento e observações.

---

## 1. Pipeline Manual Original (pré-automação no Claude Code)

O pipeline original, usado nos primeiros papers (antes da criação da skill `/beamer`), seguia estas etapas de forma manual:

1. Download do PDF e salvamento na pasta numerada correspondente
2. Upload do PDF na interface web do Claude.ai com prompt de resumo econométrico didático em português
3. Cópia manual do texto gerado para um documento Word (.docx)
4. Upload do Word no ChatGPT com prompt específico de conversão para código LaTeX Beamer
5. Cópia manual do código LaTeX gerado para o Overleaf
6. Compilação no Overleaf e verificação visual dos slides
7. Ajustes manuais (equações, tabelas, espaçamento)
8. Download do PDF final de slides compilado

**Princípios que guiavam o processo:**
- Resumo didático com forte ênfase na econometria e na intuição econômica
- Reprodução integral do conteúdo no LaTeX — nunca resumir o que já foi resumido
- Código LaTeX completo entregue em uma única passagem
- Referência histórica de qualidade: **Hausman, Leonard e Zona (1994)** (paper 14)

**Identificação:** todas as pastas que contêm apenas `.docx` (sem `.txt` LaTeX) foram processadas por este pipeline antigo e parcialmente manual.

---

## 2. Criação da Skill `/beamer`

Um arquivo (já deletado) (`Prompt Claude Code.txt`) documentava os requisitos técnicos do pipeline como briefing para migração ao Claude Code. Com base nele, foi criada a skill `/beamer`, que automatiza as 5 fases do processo:

1. **Identificação do PDF** na pasta informada
2. **Geração do resumo didático** em português (foco em econometria e intuição econômica)
3. **Salvamento do Word** (.docx) via `python-docx`
4. **Geração do código LaTeX Beamer** completo (.txt)
5. **Confirmação final** dos arquivos gerados

A skill foi registrada em `userSettings:beamer` no Claude Code. O template LaTeX de referência está em:
`C:\Users\rafael.oliveira\.claude\templates\beamer_latex.md`

**Identificação:** todas as pastas que contêm um arquivo `.txt` com código LaTeX foram processadas pelo Claude Code com a skill `/beamer`. As pastas sem `.txt` foram processadas pelo pipeline manual original. A única pasta sem nenhuma ação é a do **paper 8 — Train (2003)**, que é um livro e foi excluído explicitamente.

---

## 3. Regras Técnicas da Skill `/beamer`

- **Extração de PDF:** `pdfplumber`
- **Geração de Word:** `python-docx` — `add_heading(título, level=0)` + `add_heading(seção, level=1)` + `add_paragraph(conteúdo)`
- **Tema LaTeX:** `\usetheme{Boadilla}` com `\usepackage[portuguese]{babel}` e identificação FEA-USP
- **Equações no Word:** Unicode legível (ex: `β`, `Σᵢ γᵢⱼ ln pⱼ`) — nunca LaTeX no Word
- **Tabelas estreitas (1–3 colunas):** `\centering` apenas — `\resizebox` expande tabelas pequenas e distorce o layout
- **Tabelas largas (4+ colunas):** `\resizebox{\textwidth}{!}{...}` + `{\footnotesize}`
- **Densidade por frame:** no máximo 4 bullets e ~10 linhas totais; dividir em "(cont.)" quando exceder
- **Substituições de texto:** nunca usar `sed` no Windows (duplica backslashes) — usar Python `str.replace()`
- **Slide final obrigatório:** `\begin{frame}{Obrigado}\centering\Large Obrigado!\end{frame}`

---

## 4. Inventário de Papers

O arquivo `lista_papers_OIE.xlsx` (raiz desta pasta) é a lista canônica dos 42 artigos planejados para a disciplina. A tabela abaixo registra o status dos arquivos gerados.

Legenda: ✓ = arquivo presente; — = ausente

| Nº | Pasta / Autores (Ano) | Resumo .docx | LaTeX .txt | Pipeline |
|----|-----------------------|:------------:|:----------:|----------|
| 1 | Klein e Rubin (1947) | ✓ | — | manual |
| 2 | Barnett e Serletis (2008) | ✓ | ✓ | skill |
| 3 | Christensen, Jorgenson e Lau (1975) | ✓ | — | manual |
| 4 | Deaton e Muellbauer (1980a) | ✓ | — | manual |
| 5 | *(pasta não existe)* | — | — | — |
| 6 | Banks, Blundell e Lewbel (1997) | ✓ | — | manual |
| 7 | Lewbel e Pendakur (2009) | ✓ | ✓ | skill |
| 8 | Train (2003) | — | — | livro |
| 9 | Berry (1994) | ✓ | — | manual |
| 10 | Verboven (1996) | ✓ | ✓ | skill |
| 11 | Goldberg e Verboven (2001) | ✓ | ✓ | skill |
| 12 | BLP (1995) | ✓ | — | manual |
| 13 | *(pasta não existe)* | — | — | — |
| 14 | Hausman, Leonard e Zona (1994) | ✓ | — | manual |
| 15 | Bresnahan, Stern e Trajtenberg (1997) | ✓ | ✓ | skill |
| 16 | Chamberlain (1987) | ✓ | — | manual |
| 17 | Gandhi e Houde (2019) | ✓ | ✓ | skill |
| 18 | Reynaert e Verboven (2012) | ✓ | ✓ | skill |
| 19 | Arellano e Bond (1991) | ✓ | — | manual |
| 20 | Blundell e Bond (1998) | ✓ | — | manual |
| 21 | Olley e Pakes (1996) | ✓ | — | manual |
| 22 | Levinsohn e Petrin (2003) | ✓ | — | manual |
| 23 | Ackerberg, Caves e Frazer (2006) | ✓ | ✓ | skill |
| 24 | De Loecker e Warzynski (2012) | ✓ | ✓ | skill |
| 25 | *(pasta não existe)* | — | — | — |
| 26 | Kumbhakar (1991) | ✓ | ✓ | skill |
| 27 | *(pasta não existe)* | — | — | — |
| 28 | *(pasta não existe)* | — | — | — |
| 29 | Bresnahan (1982) | ✓ | ✓ | skill |
| 30 | Lau (1982) | ✓ | ✓ | skill |
| 31 | Nevo (1998) | ✓ | ✓ | skill |
| 32 | De Loecker e Warzynski (2009) | ✓ | ✓ | skill |
| 33 | Panzar e Rosse (1987) | ✓ | ✓ | skill |
| 34 | Baker e Bresnahan (1985) | ✓ | ✓ | skill |
| 35 | Baker e Bresnahan (1988) | ✓ | ✓ | skill |
| 36 | Bresnahan e Reiss (1990) | ✓ | ✓ | skill |
| 37 | Bresnahan e Reiss (1991) | ✓ | ✓ | skill |
| 38 | Berry (1992) | ✓ | ✓ | skill |
| 39 | Berry e Reiss (2007) | ✓ | ✓ | skill |
| 40 | Aguirregabiria e Mira (2002) | ✓ | ✓ | skill |
| 41 | Aguirregabiria e Mira (2007) | ✓ | ✓ | skill |
| 42 | Pesendorfer e Schmidt-Dengler (2010) | ✓ | ✓ | skill |

**Resumo:** 24 papers processados pela skill `/beamer`; 12 pelo pipeline manual; 1 livro (paper 8) sem output; 5 posições da numeração do curso sem pasta correspondente (5, 13, 25, 27, 28).

---

## 5. Padrão de Nomes de Arquivo

```
Pasta:  NN. Sobrenome e Sobrenome (Ano)\
Word:   Resumo Sobrenome e Sobrenome (Ano).docx
LaTeX:  Apresentacao Sobrenome e Sobrenome (Ano).txt
PDF:    [nome original do arquivo, conforme baixado]
```

Quando há mais de dois autores, usar "Sobrenome, Sobrenome e Sobrenome (Ano)" no nome do arquivo.

---

## 6. Referência de Qualidade Atual

O padrão de qualidade esperado para novos processamentos é o artigo:

**Berry (1992)** — *"Estimation of a Model of Entry in the Airline Industry"*
Pasta: `38. Berry (1992)\`

Arquivos de referência:
- `Resumo Berry (1992).docx` — padrão de resumo Word
- `Apresentacao Berry (1992).txt` — padrão de código LaTeX Beamer

> Nota histórica: durante o desenvolvimento da skill (pipeline manual), a referência usada era **Hausman, Leonard e Zona (1994)** (paper 14). A referência atual é Berry (1992).

---

## 7. Como Usar a Skill `/beamer`

Para processar um novo artigo (gerar o resumo Word e o código LaTeX Beamer):

1. Abra o Claude Code na pasta `Papers OI` (ou qualquer diretório)
2. Digite `/beamer`
3. Quando solicitado, informe o **caminho completo da pasta** onde está o PDF do artigo

Exemplo:
```
/beamer
D:\Meu Drive\Academia\2026 - Doutorado FEA-USP\Primeiro Semestre 2026\Primeiro Bimestre\Organização Industrial Empírica (ouvinte)\Papers OI\43. Sobrenome (Ano)
```

O pipeline executa automaticamente as 5 fases e salva os dois arquivos de output (`.docx` e `.txt`) na pasta informada.
