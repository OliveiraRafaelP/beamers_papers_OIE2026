# Beamers — Papers de Organização Industrial Empírica (FEA-USP, 2026)

Repositório com resumos didáticos e apresentações LaTeX Beamer dos principais artigos da disciplina **Organização Industrial Empírica** do Doutorado da FEA-USP (2026, 1º semestre).

Todo o material foi gerado com a skill `/beamer` do **Claude Code** — um pipeline automatizado que lê o PDF do artigo e produz, em sequência, um resumo em Word e o código LaTeX completo para apresentação em Beamer.

---

## Estrutura do Repositório

Cada artigo tem sua própria subpasta numerada, seguindo a ordem da ementa da disciplina:

```
NN. Sobrenome e Sobrenome (Ano)/
├── [artigo original].pdf
├── Resumo Sobrenome e Sobrenome (Ano).docx   ← resumo didático em português
└── Apresentacao Sobrenome e Sobrenome (Ano).txt  ← código LaTeX Beamer
```

O arquivo `lista_papers_OIE.xlsx` na raiz lista todos os 42 artigos planejados para a disciplina, com status de processamento. O arquivo `CLAUDE.md` documenta o pipeline em detalhe.

---

## Cobertura

| Status | Qtd | Descrição |
|--------|-----|-----------|
| ✅ Skill `/beamer` | 24 | Resumo Word + LaTeX gerados automaticamente pelo Claude Code |
| 📄 Pipeline manual | 12 | Resumo Word gerado manualmente (Claude Chat + ChatGPT + Overleaf) |
| 📚 Livro | 1 | Train (2003) — livro-texto, sem output |
| — | 5 | Posições da ementa sem paper correspondente (nºs 5, 13, 25, 27, 28) |

---

## O Pipeline `/beamer`

A skill automatiza 5 fases a partir de qualquer PDF acadêmico:

1. **Identificação do PDF** na pasta informada
2. **Geração do resumo didático** em português — ênfase em econometria e intuição econômica
3. **Salvamento do Word** (`.docx`) via `python-docx`
4. **Geração do código LaTeX Beamer** completo (`.txt`) — tema Boadilla, FEA-USP
5. **Confirmação** dos arquivos gerados

O código LaTeX produzido pode ser colado diretamente no [Overleaf](https://www.overleaf.com) para compilação imediata.

### Como usar em novos artigos

1. Instale o [Claude Code](https://claude.ai/code)
2. Instale as dependências Python:
   ```
   pip install pdfplumber python-docx
   ```
3. Baixe os arquivos da skill em **[OliveiraRafaelP/claude-beamer-skill](https://github.com/OliveiraRafaelP/claude-beamer-skill)** e copie para o seu usuário:
   - `commands/beamer.md` → `~/.claude/commands/beamer.md`
   - `templates/beamer_latex.md` → `~/.claude/templates/beamer_latex.md`
4. No Claude Code, digite `/beamer` e informe o caminho da pasta do artigo

O repositório [claude-beamer-skill](https://github.com/OliveiraRafaelP/claude-beamer-skill) contém a documentação completa da skill, instruções de instalação e personalização.

---

## Referência de Qualidade

O padrão de resumo e apresentação adotado é o artigo **Berry (1992)** — *"Estimation of a Model of Entry in the Airline Industry"* (pasta `38. Berry (1992)`).

---

## Autor

**Rafael Pereira Oliveira**
Doutorando — Faculdade de Economia, Administração e Contabilidade (FEA-USP)
