# 🪟 Atividade 01 — Relatório Técnico: Formatação e Instalação do Sistema Operacional Windows

![Disciplina](https://img.shields.io/badge/Disciplina-Sistemas_Operacionais-blue)
![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-brightgreen)
![Versão](https://img.shields.io/badge/Vers%C3%A3o-3.0.0--Avan%C3%A7ado-orange)
![OS Target](https://img.shields.io/badge/OS_Target-Windows_10%2F11-0078D6)

---

## 📑 Índice
1. [Sobre a Atividade](#-sobre-a-atividade)
2. [Cenário Proposto e Objetivos](#-cenário-proposto-e-objetivos)
3. [Arquitetura Interna do Windows (Kernel x User Mode)](#-arquitetura-interna-do-windows-kernel-x-user-mode)
4. [Fluxograma Completo do Processo (Mermaid)](#-fluxograma-completo-do-processo-mermaid)
5. [Detalhamento Técnico das Fases de Instalação](#-detalhamento-técnico-das-fases-de-instalação)
   - [Fase 1: Preparação e Boot (POST, UEFI, Secure Boot)](#fase-1-preparação-e-boot-post-uefi-secure-boot)
   - [Fase 2: Particionamento e Sistemas de Arquivos (GPT, NTFS, NVMe)](#fase-2-particionamento-e-sistemas-de-arquivos-gpt-ntfs-nvme)
   - [Fase 3: Cópia e Implantação da Imagem (`install.wim` / Kernel)](#fase-3-cópia-e-implantação-da-imagem-installwim--kernel)
   - [Fase 4: Inicialização do SO, Drivers e OOBE](#fase-4-inicialização-do-so-drivers-e-oobe)
6. [Análise de Estrutura de Pastas e Partições Geradas](#-análise-de-estrutura-de-pastas-e-partições-geradas)
7. [Tabela Comparativa Tecnológica](#-tabela-comparativa-tecnológica)
8. [Matriz de Conceitos da Disciplina](#-matriz-de-conceitos-da-disciplina)
9. [Guia de Resolução de Problemas (Troubleshooting)](#-guia-de-resolução-de-problemas-troubleshooting)
10. [Checklist Completo de Verificação](#-checklist-completo-de-verificação)
11. [Conclusão e Considerações Finais](#-conclusão-e-considerações-finais)

---

## 📌 Sobre a Atividade

> **Curso:** Análise e Desenvolvimento de Sistemas  
> **Disciplina:** Estrutura e Arquitetura de Sistemas Operacionais  
> **Professor:** Me. Deivison S. Takatu  

> [!NOTE]  
> Este documento apresenta uma análise técnica minuciosa sobre a formatação e instalação limpa (*Clean Install*) do Microsoft Windows. O trabalho correlaciona as etapas práticas de bancada com os conceitos teóricos de Arquitetura de Sistemas Operacionais (gerenciamento de memória, modos de execução do processador, abstração de hardware, tabelas de partição e sistemas de arquivos).

---

## 💻 Cenário Proposto e Objetivos

### Cenário
Um computador corporativo deu entrada no laboratório de manutenção apresentando lentidão severa, suspeita de corrupção do sistema de arquivos e arquivos maliciosos instalados. A equipe técnica determinou a necessidade de um procedimento de **Formatação e Instalação Limpa do Windows 11 64-bit**.

### Objetivos Técnicos
1. Garantir a integridade do hardware através do diagnóstico de *firmware*.
2. Apagar com segurança todas as tabelas lógicas anteriores e reestruturar o disco usando padrões modernos (**GPT** / **NTFS**).
3. Deslocar o núcleo (*Kernel*) e a camada de abstração de hardware (**HAL**) para a unidade de armazenamento principal.
4. Mapear o processo prático com a arquitetura teórica estudada em aula.

---

## 🧠 Arquitetura Interna do Windows (Kernel x User Mode)

Antes de detalhar o processo de instalação, é fundamental compreender a arquitetura do sistema que está sendo implantado. O Windows utiliza uma arquitetura baseada em **Kernel Híbrido**.

```mermaid
graph TD
    subgraph UserMode ["Modo Usuário (Ring 3 - Acesso Limitado)"]
        A1[Aplicações do Usuário]
        A2[Sub-sistemas de Ambiente - Win32, WSL]
        A3[DLLs de Sistema - ntdll.dll, kernel32.dll]
    end

    subgraph KernelMode ["Modo Kernel (Ring 0 - Acesso Total ao Hardware)"]
        B1[Executive Services - Gerenciamento de Memória, Processos, E/S]
        B2[Kernel do Windows - ntoskrnl.exe]
        B3[Drivers de Dispositivo - Kernel Mode Drivers]
        B4[HAL - Camada de Abstração de Hardware]
    end

    subgraph Hardware ["Hardware Físico"]
        C1[CPU / RAM / NVMe / GPU / Chipset]
    end

    UserMode -->|System Calls / Interrupções| KernelMode
    KernelMode --> Hardware
