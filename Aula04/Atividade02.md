[gemini-code-1787585113591.md](https://github.com/user-attachments/files/31381481/gemini-code-1787585113591.md)
# 🖥️ Atividade 02 — Sistemas Operacionais Derivados e Análise Comparativa

![Disciplina](https://img.shields.io/badge/Disciplina-Sistemas_Operacionais-blue)
![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-brightgreen)
![Versão](https://img.shields.io/badge/Vers%C3%A3o-2.0.0-orange)
![Licença](https://img.shields.io/badge/Licen%C3%A7a-MIT-yellow)

---

## 📑 Índice
1. [Sobre a Atividade](#-sobre-a-atividade)
2. [Sistemas Operacionais Pesquisados](#-sistemas-operacionais-pesquisados)
3. [Arquitetura de Linhagem (Mermaid)](#-arquitetura-de-linhagem-mermaid)
4. [Tabela Comparativa Avançada](#-tabela-comparativa-avançada)
5. [Detalhamento de Modificações](#-detalhamento-de-modificações)
6. [Checklist de Requisitos](#-checklist-de-requisitos)
7. [Conclusão](#-conclusão)

---

## 📌 Sobre a Atividade

> **Curso:** Análise e Desenvolvimento de Sistemas  
> **Disciplina:** Estrutura e Arquitetura de Sistemas Operacionais  
> **Professor:** Me. Deivison S. Takatu  

> [!NOTE]  
> O objetivo desta atividade é identificar **5 Sistemas Operacionais** desenvolvidos a partir de outro sistema base (reaproveitando kernel, arquitetura ou estrutura) e analisar comparativamente suas diferenças, inovações e casos de uso.

---

## 🔍 Sistemas Operacionais Pesquisados

1. **Android** (Base: *Kernel Linux*)[cite: 1]
2. **macOS** (Base: *Darwin / FreeBSD / Mach*)[cite: 1]
3. **Ubuntu** (Base: *Debian GNU/Linux*)[cite: 1]
4. **SteamOS 3.x** (Base: *Arch Linux*)[cite: 1]
5. **Orbis OS** (Base: *FreeBSD 9.0*)[cite: 1]

---

## 🧬 Arquitetura de Linhagem (Mermaid)

```mermaid
graph TD
    A[Kernel Linux / GNU] -->|Kernel modificado| B(Android)
    A -->|Distribuição base| C(Debian)
    C -->|Foco em facilidade e UX| D(Ubuntu)
    
    E[BSD / Unix] -->|Darwin / Mach| F(macOS)
    E -->|FreeBSD 9.0| G(Orbis OS - PS4)
    
    H[Arch Linux] -->|Immutable OS + Proton| I(SteamOS 3.x)

    style B fill:#3DDC84,stroke:#333,stroke-width:1px,color:#000
    style D fill:#E95420,stroke:#333,stroke-width:1px,color:#fff
    style F fill:#000000,stroke:#fff,stroke-width:1px,color:#fff
    style I fill:#1b2838,stroke:#66c0f4,stroke-width:1px,color:#fff
    style G fill:#003791,stroke:#333,stroke-width:1px,color:#fff
