# 📚 StudyHub — Controle de Estudos

> Um painel pessoal, leve e offline-first para organizar apostilas, matérias, conteúdos e exercícios de estudo — feito para quem está se preparando para o vestibular.

![status](https://img.shields.io/badge/status-em%20uso-2a7d5f) ![tipo](https://img.shields.io/badge/tipo-app%20local-8b5cf6) ![dados](https://img.shields.io/badge/dados-100%25%20locais-d49a3a)

---

## ✨ Visão Geral

O **StudyHub** é um aplicativo de página única (single-file HTML/CSS/JS) que roda direto no navegador, sem servidor, sem login e sem enviar nada para a nuvem. Todos os seus dados — apostilas, matérias, conteúdos, exercícios e progresso — ficam salvos localmente no seu próprio dispositivo.

Ele foi pensado para resolver um problema simples: **estudar para o vestibular gera muito conteúdo espalhado**, e é fácil perder a visão de conjunto — o que já foi visto, o que está pendente, o que é prioridade e o que precisa de revisão.

---

## 🗂️ Estrutura de Dados

O sistema organiza tudo em uma hierarquia de 4 níveis:

```
📘 Apostila
 └── 📚 Matéria           (ex: Biologia, Química, Matemática...)
      └── 📝 Conteúdo      (ex: "A questão ambiental (I)", Aula 5, Parte L)
           └── 📋 Exercício (ex: "Exercícios de Aula" — 5 questões, 3 resolvidas)
```

Cada nível carrega suas próprias informações:

| Nível | Campos principais |
|---|---|
| **Apostila** | nome, descrição, cor, data de criação |
| **Matéria** | nome, **prioridade** (alta / média / baixa / nenhuma) |
| **Conteúdo** | parte, aula, título, status, **prioridade**, observações, data de conclusão, marcação de revisão |
| **Exercício** | nome, nº de questões, nº resolvidas, status |

---

## 🚦 Prioridades e Status

- **Prioridade** (`alta` 🔴 · `media` 🟡 · `baixa` 🔵 · `nenhuma` ⚪) indica o quão recorrente/importante aquele conteúdo costuma ser em provas de vestibular.
- **Status** (`pendente` · `estudando` · `concluido`) acompanha o andamento real do estudo.
- **🔖 Revisar depois** é uma marcação independente — não interfere no progresso nem na prioridade, só sinaliza "quero voltar aqui".

---

## 🧭 Navegação do App

| Tela | O que mostra |
|---|---|
| **📚 Apostilas** | Cards com todas as apostilas, progresso geral e atalho para revisão |
| **📘 Apostila** | Matérias daquela apostila, gráficos de progresso (rosca + barras), ordenadas por prioridade |
| **📖 Matéria** | Conteúdos agrupados por "parte", ordenados por prioridade e número da aula |
| **📝 Conteúdo** | Detalhes completos + lista de exercícios com checkbox animado para marcar questões resolvidas |
| **📈 Estatísticas** | Ranking geral de apostilas e de matérias por % de conclusão |
| **📥 Importações** | Importa dados colando texto simples ou JSON |
| **⚙️ Configurações** | Exportar, fazer backup e restaurar dados |

---

## 💾 Backup e Exportação — por Apostila

Diferente de um backup único e genérico, o StudyHub **gera um arquivo `.json` separado para cada apostila**:

```
studyhub_backup_apostila_2_2026-07-05.json
studyhub_backup_apostila_etapa_x4_2026-07-05.json
```

Isso evita misturar apostilas diferentes em um único arquivo e facilita:
- Guardar cada apostila isoladamente
- Restaurar seletivamente
- Compartilhar apenas uma apostila específica, se quiser

A restauração aceita **múltiplos arquivos ao mesmo tempo** — basta selecionar todos os backups e o sistema funde tudo de volta, apostila por apostila, sem duplicar conteúdos já existentes.

---

## 🔍 Busca e Filtros

A barra de pesquisa cobre apostilas, matérias, conteúdos e exercícios simultaneamente, e pode ser combinada com filtros de:
- Apostila específica
- Prioridade (alta / média / baixa / nenhuma)
- Status (pendente / estudando / concluído)
- Marcação de revisão

---

## 🎨 Aparência

- Tema **claro** e **escuro**, com transição suave e alternância pela sidebar.
- Cada apostila tem uma cor de identidade própria, usada em barras de progresso, gráficos e destaques.
- Totalmente responsivo — funciona bem em desktop e celular (com menu retrátil).

---

## 🔒 Privacidade

Nenhum dado sai do seu navegador. Não há conta, login ou envio para servidores externos — tudo vive no `localStorage` do dispositivo, com exportação manual quando você quiser guardar uma cópia em arquivo.

---

## 🛠️ Stack Técnica

- **HTML + CSS + JavaScript puro** (zero frameworks, zero build step)
- Fontes: [Syne](https://fonts.google.com/specimen/Syne) (títulos) + [Lora](https://fonts.google.com/specimen/Lora) (texto)
- Gráficos desenhados via `<canvas>` nativo (sem bibliotecas externas)
- Armazenamento via `localStorage`, com import/export em JSON

---

<p align="center"><i>Feito para organizar a reta final antes do vestibular — um conteúdo de cada vez. 📖</i></p>
