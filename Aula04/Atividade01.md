# 🪟 Atividade 01 — Formatação e Instalação de um Sistema Operacional (Windows)

![Disciplina](https://img.shields.io/badge/Disciplina-Sistemas_Operacionais-blue)
![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-brightgreen)
![Versão](https://img.shields.io/badge/Vers%C3%A3o-2.0.0-orange)
![OS](https://img.shields.io/badge/OS-Windows_10%2F11-0078D6)

---

## 📑 Índice
1. [Sobre a Atividade](#-sobre-a-atividade)
2. [Cenário e Contexto](#-cenário-e-contexto)
3. [Fluxograma do Processo (Mermaid)](#-fluxograma-do-processo-mermaid)
4. [Fases da Instalação e Conceitos de SO](#-fases-da-instalação-e-conceitos-de-so)
5. [Tabela de Conceitos e Arquitetura](#-tabela-de-conceitos-e-arquitetura)
6. [Checklist Pós-Instalação](#-checklist-pós-instalação)
7. [Conclusão](#-conclusão)

---

## 📌 Sobre a Atividade

> **Curso:** Análise e Desenvolvimento de Sistemas  
> **Disciplina:** Estrutura e Arquitetura de Sistemas Operacionais  
> **Professor:** Me. Deivison S. Takatu  

> [!NOTE]  
> O objetivo desta atividade é descrever, analisar e apresentar o processo completo de formatação e instalação do sistema operacional Windows em um computador, relacionando rigorosamente cada etapa aos conceitos fundamentais estudados sobre Arquitetura de Sistemas Operacionais.

---

## 💻 Cenário Proposto

Um computador foi recebido para ser formatado e preparado para uma nova instalação limpa (*Clean Install*) do Windows. O processo abrange desde a inicialização de baixo nível do firmware da máquina até a configuração final do ambiente do usuário, integrando conceitos de gerenciamento de hardware, sistemas de arquivos e o papel central do Kernel.

---

## 📈 Fluxograma do Processo de Instalação (Mermaid)

```mermaid
flowchart TD
    A[1. Inicialização / Firmware] -->|POST & UEFI/BIOS| B[2. Boot via Mídia Externa]
    B -->|Carrega Mini-SO de Instalação| C[3. Particionamento e Formatação]
    C -->|Criação de Estrutura NTFS / GPT| D[4. Cópia e Descompactação de Arquivos]
    D -->|Gravação no Disco Rígido| E[5. Configuração Inicial - OOBE]
    E -->|Instalação de Drivers & HAL| F[6. Sistema Pronto para Uso]

    style A fill:#0078D6,stroke:#333,stroke-width:1px,color:#fff
    style C fill:#1b2838,stroke:#66c0f4,stroke-width:1px,color:#fff
    style F fill:#3DDC84,stroke:#333,stroke-width:1px,color:#000
