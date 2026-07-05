<p align="center">
  <h1 align="center">Study<span style="color:#2a7d5f">Hub</span></h1>
  <p align="center">A complete study control system for managing study materials, subjects, content, and exercises with progress tracking.</p>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/version-7.0-blue" alt="Version">
  <img src="https://img.shields.io/badge/license-MIT-green" alt="License">
  <img src="https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white" alt="HTML5">
  <img src="https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white" alt="CSS3">
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black" alt="JavaScript">
</p>

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
  - [Apostilas (Study Materials)](#apostilas-study-materials)
  - [Subjects (Materias)](#subjects-materias)
  - [Content (Conteudos)](#content-conteudos)
  - [Exercises (Exercicios)](#exercises-exercicios)
  - [Priority System](#priority-system)
  - [Status Tracking](#status-tracking)
  - [Dashboard & Statistics](#dashboard--statistics)
  - [Search & Filters](#search--filters)
  - [Import & Export](#import--export)
  - [Dark & Light Mode](#dark--light-mode)
  - [Responsive Design](#responsive-design)
  - [Data Persistence](#data-persistence)
  - [Charts & Visualizations](#charts--visualizations)
  - [Navigation](#navigation)
  - [Animated +1 Checkbox](#animated-1-checkbox)
  - [Notifications](#notifications)
  - [Data Migration](#data-migration)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [License](#license)

---

## Overview

**StudyHub** is a single-file, zero-dependency study management application built entirely with vanilla HTML, CSS, and JavaScript. It provides a hierarchical organization system for tracking study materials — from high-level apostilas (study guides) down to individual exercises — with real-time progress tracking, priority management, and data visualization.

Everything runs client-side in the browser with no server required. All data is stored in `localStorage`.

---

## Features

### Apostilas (Study Materials)

The top-level organizational unit. Each apostila represents a study guide or book.

| Action | Description |
|--------|-------------|
| **Create** | Name, description, and color selection from a 10-color palette |
| **Read** | Card-based view showing subject count, content progress, and question progress |
| **Update** | Edit name, description, and color at any time |
| **Delete** | Cascading deletion with confirmation — removes all nested subjects, content, and exercises |

### Subjects (Materias)

Nested inside apostilas, subjects represent individual disciplines (e.g., Mathematics, Biology).

| Action | Description |
|--------|-------------|
| **Create** | Name and priority level assignment |
| **Read** | Card view with progress bars for content completion and exercise progress |
| **Update** | Edit name, priority, and move between apostilas |
| **Delete** | Cascading deletion with confirmation |

**Sorting:** Subjects are automatically sorted by priority (alta > media > baixa > nenhuma), then alphabetically within the same priority level.

**Visual indicators:** High-priority subjects get a red left border, medium gets amber, and low gets the accent color.

### Content (Conteudos)

The individual study units nested inside subjects. Each content item represents a lesson or topic.

| Action | Description |
|--------|-------------|
| **Create** | Part number, lesson number, title, status, priority, and optional notes |
| **Read** | Grouped by part (PARTE L, PARTE M, etc.), sorted by priority then lesson number |
| **Update** | Edit all fields including status transitions with automatic date tracking |
| **Delete** | Confirmation dialog before removal |
| **Toggle** | Quick-complete toggle via the cycle button (pending / completed) |

**Content detail view** shows: apostila name, subject name, both priority levels (subject + content), part, lesson, status badge, completion date, exercise count, and notes.

### Exercises (Exercicios)

Nested inside content items, exercises track question sets and solved counts.

| Action | Description |
|--------|-------------|
| **Create** | Name and total question count |
| **Read** | Card with progress bar, percentage, and status badge |
| **Update** | Edit name, total questions, and solved count (auto-clamped to valid range) |
| **Delete** | Confirmation dialog before removal |
| **+1 Increment** | Animated checkbox to mark one question solved at a time |

**Auto-status:** Exercise status automatically updates based on solved count:
- `0 solved` — Pendente
- `1 to (total-1) solved` — Estudando
- `all solved` — Concluido

---

### Priority System

Four priority levels available for both **subjects** and **content**:

| Level | Label | Visual | Border Color |
|-------|-------|--------|-------------|
| `alta` | High | Red badge + left border | `#d1453b` |
| `media` | Medium | Amber badge + left border | `#d49a3a` |
| `baixa` | Low | Green badge + left border | `#2a7d5f` |
| `nenhuma` | None | Gray badge, no border | `#9494a8` |

Priority affects:
- **Display order** in content lists (high priority items appear first)
- **Visual emphasis** via colored left borders and gradient backgrounds
- **Statistics** — dedicated counters for high and medium priority items in the dashboard
- **Ranking** — subject ranking sorts by priority first, then completion percentage

---

### Status Tracking

Three states for content items:

| Status | Badge Color | Description |
|--------|------------|-------------|
| `pendente` | Amber/Warning | Not yet started |
| `estudando` | Green/Accent | In progress |
| `concluido` | Green/Success | Completed |

Completion automatically records a timestamp (`dataConclusao`). Reverting from completed clears the date.

---

### Dashboard & Statistics

The **Estatisticas** page provides:

- **Global overview cards:** Total apostilas, total content (completed/pending), total questions (solved/remaining), overall progress percentage, high-priority subject count, high-priority content count
- **Donut chart:** Overall progress visualization with color-coded thresholds (green >= 75%, amber >= 40%, red < 40%)
- **Bar chart:** Progress per apostila, sorted by completion
- **Ranking list:** All apostilas ranked by progress percentage with detailed breakdowns
- **Subject ranking:** All subjects across all apostilas ranked by priority first, then progress

---

### Search & Filters

Global search and filtering available from the toolbar:

| Filter | Description |
|--------|-------------|
| **Text search** | Matches against apostila names, subject names, content titles, lesson numbers, part names, and exercise names. 300ms debounce. |
| **Apostila filter** | Dropdown to show content from a specific apostila only |
| **Priority filter** | Filter by alta, media, baixa, or nenhuma |
| **Status filter** | Filter by pendente, estudando, or concluido |

All filters combine (stack) for precise results. A clear button resets the search field.

---

### Import & Export

#### Text Import

Paste structured text to bulk-import content. The parser recognizes:
- `APOSTILA X` — creates a new apostila
- `ALL CAPS LINES` — creates a new subject (auto-capitalized)
- `PARTE X` — sets the current part
- `Aula N: Title` — creates a content item
- Other lines under a content item — creates exercises

A preview step shows detected counts before confirming.

#### JSON Import

Two modes:
- **Inline** (Import page) — paste JSON into a textarea
- **Modal** — accessible from Settings or any view

JSON format:

```json
{
  "apostilas": [
    {
      "nome": "Apostila 1",
      "descricao": "Description",
      "cor": "#2a7d5f",
      "materias": [
        {
          "nome": "Subject",
          "prioridade": "alta",
          "conteudos": [
            {
              "parte": "L",
              "aula": "5",
              "titulo": "Topic Title",
              "status": "pendente",
              "prioridade": "media",
              "exercicios": [
                { "nome": "Exercise Set", "questoes": 10, "resolvidas": 0 }
              ]
            }
          ]
        }
      ]
    }
  ]
}
