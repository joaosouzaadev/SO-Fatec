[gemini-code-1787583657162.md](https://github.com/user-attachments/files/31381750/gemini-code-1787583657162.md)
# Atividade 02 - Sistemas Operacionais Derivados e Análise Comparativa

**Disciplina:** Estrutura e Arquitetura de Sistemas Operacionais  
**Professor:** Me. Deivison S. Takatu  

---

## 1. Pesquisa: Sistemas Operacionais e Suas Bases

Abaixo estão selecionados 5 Sistemas Operacionais desenvolvidos com base em outros sistemas, reaproveitando seus kernels, arquiteturas ou estruturas:

1. **Android**: Desenvolvido pelo Google, utiliza uma versão modificada do **Kernel Linux** como sua base subjacente para gerenciamento de memória, processos e drivers de hardware.
2. **macOS**: Desenvolvido pela Apple, utiliza o sistema **Darwin**, que por sua vez é baseado no **FreeBSD** e na arquitetura de microkernel **Mach** (família Unix).
3. **Ubuntu**: Uma das distribuições Linux mais populares para desktops e servidores, desenvolvida pela Canonical a partir da base do **Debian**.
4. **SteamOS 3.x**: Sistema operacional para jogos desenvolvido pela Valve (utilizado no Steam Deck), baseado na distribuição **Arch Linux**.
5. **Orbis OS**: Sistema operacional proprietário utilizado no console **PlayStation 4** (PS4), desenvolvido pela Sony a partir do **FreeBSD 9.0**.

---

## 2. Tabela Comparativa

| Sistema Operacional Derivado | Sistema Base | Principais Diferenças e Modificações |
| :--- | :--- | :--- |
| **Android** | Kernel Linux | Substituiu o ambiente de usuário tradicional Linux (GNU/X11) por uma máquina virtual própria (ART / Dalvik), biblioteca C simplificada (Bionic) e um framework de aplicações voltado para dispositivos móveis e telas sensíveis ao toque. |
| **macOS** | FreeBSD / Mach (Darwin) | Adicionou uma interface gráfica proprietária (Aqua), frameworks exclusivos (Cocoa, Metal) e uma camada profunda de integração com o ecossistema de hardware e software da Apple. |
| **Ubuntu** | Debian | Foca em maior facilidade de uso para usuários finais, ciclo de lançamentos fixo e previsível (a cada 6 meses), ambiente de desktop customizado e inclusão por padrão de drivers proprietários e codecs de mídia. |
| **SteamOS 3.x** | Arch Linux | Adicionou o ambiente imersivo para jogos (*Gamescope*), sistema de arquivos somente leitura com atualizações atômicas A/B e a camada de compatibilidade **Proton** para executar jogos do Windows no Linux. |
| **Orbis OS** | FreeBSD 9.0 | Removeu componentes gerais do Unix, adicionou drivers de hardware customizados para a GPU e APU do console, e implementou APIs de renderização de baixo nível (GNM/GNMX) e gerenciamento de memória exclusivo para jogos. |

---

## 3. Conclusão

Conforme discutido em aula, o reaproveitamento da estrutura de um sistema operacional existente reduz custos de desenvolvimento, traz maior estabilidade e segurança prévias, e permite que os desenvolvedores foquem nas particularidades do hardware ou nas necessidades específicas do público-alvo do novo sistema.
