# aliciasoliveira.github.io

Página pessoal (CV online) em **https://aliciasoliveira.github.io/**, feita com [Hugo](https://gohugo.io) e o tema [hugo-resume](https://github.com/eddiewebb/hugo-resume).

Cada `git push` para `main` publica o site automaticamente em cerca de 1 minuto.

---

## Onde está cada coisa

| Quero mudar…                          | Ficheiro                                  |
|---------------------------------------|-------------------------------------------|
| Texto de apresentação (topo)          | `content/_index.md`                       |
| Nome, email, localização, LinkedIn    | `hugo.toml`                               |
| Ordem / quais secções aparecem        | `hugo.toml` → `sections = [...]`          |
| Experiência profissional              | `data/experience.json`                    |
| Formação                              | `data/education.json`                     |
| Publicações                           | `content/publications/*.md` (um por artigo) |
| Talks & Events                        | `data/talks.json`                         |
| Skills                                | `data/skills.json`                        |
| Línguas                               | `data/languages.json`                     |
| Foto                                  | `static/img/profile.png`                  |
| Títulos das secções no menu           | `i18n/en.yaml`                            |

As entradas aparecem na página **pela ordem em que estão no ficheiro**, por isso as mais recentes vão sempre **no topo**.

> Não é preciso mexer em `themes/` nem em `layouts/`.

---

## 1. Ver as alterações no computador (antes de publicar)

```bash
cd ~/Documents/GitHub/aliciasoliveira.github.io
hugo server
```

Abre **http://localhost:1313/**. A página recarrega sozinha sempre que guardas um ficheiro. Para parar: `Ctrl+C`.

Se aparecer um erro no terminal, quase sempre é uma vírgula ou aspa em falta num `.json` (ver [Problemas comuns](#problemas-comuns)).

---

## 2. Editar o conteúdo

### Adicionar um evento / palestra — `data/talks.json`

Copia este bloco e cola-o **logo a seguir ao `[`** no início do ficheiro:

```json
    {
        "title": "Nome do evento",
        "location": "Cidade, País",
        "range": "Outubro 2026",
        "summary": "O que fizeste. Podes usar *itálico* e **negrito**.",
        "links": ["https://link-do-evento.pt/"]
    },
```

- `links` é opcional (podes pôr vários: `["https://a", "https://b"]`) ou apagar a linha.
- Atenção à **vírgula** no fim do `}` — separa este bloco do seguinte.

### Adicionar uma experiência — `data/experience.json`

```json
    {
        "role": "Cargo",
        "company": "Instituição",
        "summary": "- Primeira tarefa\n- Segunda tarefa",
        "range": "Janeiro 2027 - Present"
    },
```

`\n- ` cria um novo ponto da lista.

### Adicionar formação — `data/education.json`

```json
    {
        "school": "[University of Minho](https://www.uminho.pt)",
        "degree": "Nome do curso",
        "major": "**Thesis:** Título da tese",
        "range": "2025 - 2029"
    },
```

### Adicionar uma publicação — `content/publications/`

Cria um ficheiro novo, por exemplo `content/publications/nome-curto.md`:

```markdown
---
title: "Título completo do artigo"
date: 2027-03-01
pubtype: "Paper"
featured: true
description: "Autor A, **Alícia Oliveira**, Autor C. *Nome da Conferência*, 2027."
tags: ["HPC", "LLMs"]
link: "https://doi.org/..."
weight: 50
---
Texto opcional que aparece na página própria do artigo (resumo, links, etc.).
```

- `pubtype`: `Paper`, `Preprint`, `Poster`, `Talk`… (aparece antes do título).
- `featured: true` → aparece na página principal.
- `weight` → ordem: **número mais baixo aparece primeiro**. Os atuais usam 100, 200, 300, 400; para pôr um novo no topo usa um valor menor (ex.: 50).
- `link` é opcional.
- Só o ano da `date` é mostrado.

### Skills — `data/skills.json`

Cada grupo tem um título e uma lista:

```json
{"name": "Kubernetes"},
```

### Mudar a foto

Substitui `static/img/profile.png` por outra imagem quadrada com o **mesmo nome**.

### Mudar o texto do topo

Edita o parágrafo em `content/_index.md` (tudo o que está depois do segundo `---`).

---

## 3. Publicar

```bash
cd ~/Documents/GitHub/aliciasoliveira.github.io
git add -A
git commit -m "Adiciona evento X"
git push
```

Depois do push, acompanha em
**https://github.com/aliciasoliveira/aliciasoliveira.github.io/actions** — quando o workflow *Deploy Hugo site to GitHub Pages* ficar verde ✅, o site está atualizado.
Se não vires a mudança, faz refresh forçado no browser (**⌘ + Shift + R**).

---

## Problemas comuns

**`hugo server` dá erro num ficheiro `.json`**
Falta ou sobra uma vírgula/aspa. Regras:
- Entre dois blocos `{ ... }` há uma vírgula; depois do **último** não há.
- Todo o texto vai entre aspas `"..."`. Se precisares de aspas dentro do texto, usa `\"` ou *itálico*.

**O workflow no GitHub ficou vermelho ❌**
Abre-o em *Actions* e vê o passo *Build* — o erro é o mesmo que verias com `hugo server`. Corrige, faz commit e push outra vez.

**O site dá 404 ou mostra uma versão antiga**
Confirma em *Settings → Pages* que **Source = GitHub Actions** (não "Deploy from a branch"). Depois, em *Actions → Deploy Hugo site to GitHub Pages*, carrega em **Run workflow**.

**O `git push` pede username/password**
- Username: `aliciasoliveira`
- Password: um **Personal Access Token** (https://github.com/settings/tokens) com os scopes `repo` e `workflow`.

**Não tenho o Hugo instalado (ex.: outro computador)**
```bash
brew install hugo
```
Não é obrigatório — podes editar os ficheiros diretamente no GitHub (ícone ✏️) e o site é publicado na mesma.
