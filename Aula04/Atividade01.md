
# Atividade 01 — Formatação e Instalação de um Sistema Operacional Windows

**Disciplina:** Estrutura e Arquitetura de Sistemas Operacionais
**Cenário:** um computador foi recebido para ser formatado e preparado para uma nova instalação do Windows. O documento a seguir descreve todo o processo, desde o momento em que a máquina é ligada até o Windows estar instalado e pronto para uso, relacionando cada etapa aos conceitos de Sistemas Operacionais estudados em aula.

---

## 1. Descrição Geral do Processo

De forma resumida, o processo percorre as seguintes fases: o computador é ligado e o firmware (BIOS/UEFI) assume o controle; a mídia de instalação é reconhecida e um mini sistema (o instalador) é carregado na memória; o instalador identifica o hardware disponível; o usuário escolhe/prepara a unidade de destino, que é particionada e formatada; os arquivos do Windows são copiados e expandidos para essa unidade; o sistema é configurado e reinicia, agora inicializando pelo próprio disco; o kernel do Windows assume o controle definitivo da máquina; drivers de dispositivo são carregados e configurados; e, por fim, o sistema fica pronto para o usuário executar aplicações.

Esse processo é, na prática, a transição de um conjunto de peças de hardware "mudas" para uma máquina capaz de gerenciar recursos, executar múltiplos programas e mediar a comunicação entre usuário e hardware — que é exatamente o papel de um Sistema Operacional.

---

## 2. Conceitos Envolvidos

### 2.1 Componentes do Sistema Operacional

Durante a instalação e a configuração do Windows, diversos componentes do SO entram em ação, cada um responsável por gerenciar um recurso específico da máquina:

| Componente | Recurso que gerencia | Momento em que atua |
|---|---|---|
| **Kernel** | CPU, memória, escalonamento de processos | Desde o carregamento do instalador até o funcionamento definitivo do sistema |
| **Gerenciador de memória** | RAM (alocação para o instalador, depois para o SO instalado) | Durante toda a execução do instalador e após o boot final |
| **Sistema de arquivos (NTFS)** | Organização e localização de dados no disco | Na formatação e na cópia dos arquivos de instalação |
| **Gerenciador de Entrada/Saída (I/O Manager)** | Comunicação com teclado, mouse, monitor, disco, rede | Do início ao fim, sempre que há interação com dispositivos |
| **Drivers de dispositivo** | Tradução entre comandos genéricos do SO e hardware específico | Reconhecimento de hardware e após a instalação |
| **Bootloader (Windows Boot Manager)** | Localização e carregamento do kernel | No primeiro boot após a cópia dos arquivos |
| **Serviços do sistema (services.exe)** | Processos em segundo plano (rede, plug-and-play, etc.) | Na configuração inicial e no uso normal do sistema |

Esses componentes são necessários porque nenhum hardware "sabe" sozinho como armazenar arquivos de forma organizada, gerenciar múltiplos programas concorrendo pela CPU, ou entender comandos de um teclado ou disco — é o SO que fornece essa camada de abstração e controle.

### 2.2 Kernel: o Núcleo do Sistema

O kernel é o componente mais privilegiado do Windows, responsável por gerenciar diretamente CPU, memória e dispositivos, e por servir de intermediário entre o software e o hardware.

- **Quando passa a atuar:** um kernel mínimo já atua durante o próprio instalador (o setup do Windows roda sobre um ambiente de pré-instalação, o *Windows PE*, que possui seu próprio kernel reduzido). O kernel definitivo do Windows (`ntoskrnl.exe`) passa a atuar no primeiro boot a partir do disco recém-instalado, quando o bootloader o carrega na memória.
- **Como gerencia os recursos:** o kernel controla o escalonamento de processos (decidindo qual processo usa a CPU e por quanto tempo), a alocação e proteção de áreas de memória para cada processo, e a fila de requisições de entrada/saída para os dispositivos.
- **Como faz a comunicação entre software e hardware:** o kernel expõe chamadas de sistema (*system calls*) que os programas usam para solicitar recursos (abrir um arquivo, alocar memória, escrever na tela); é o kernel, e não o programa, quem efetivamente acessa o hardware, por meio dos drivers.
- **Recursos controlados durante a instalação:** memória RAM disponível para o instalador, acesso exclusivo ao disco de destino (para evitar corrupção durante a formatação/cópia), e os dispositivos de I/O necessários para o instalador funcionar (teclado, mouse, monitor, unidade de instalação).

### 2.3 Modos de Execução

O Windows opera com dois modos principais de execução da CPU:

- **Modo Kernel (privilegiado):** onde roda o núcleo do SO e os drivers de dispositivo. Nesse modo há acesso irrestrito à memória e ao hardware.
- **Modo Usuário (não privilegiado):** onde rodam os programas comuns, incluindo o próprio instalador do Windows (setup.exe) e, depois, os aplicativos do usuário. Programas em modo usuário não podem acessar hardware diretamente; precisam solicitar ao kernel por meio de *system calls*.

**Momentos em que aparecem na instalação:** o processo do instalador (`setup.exe`) roda em modo usuário, mas toda vez que precisa gravar dados no disco, alocar memória ou detectar hardware, ele faz uma chamada de sistema que transfere a execução para o modo kernel, que executa a operação privilegiada e devolve o controle ao modo usuário.

**Por que o SO não permite acesso direto e irrestrito ao hardware:** se qualquer programa pudesse acessar o hardware livremente, um erro ou uma ação maliciosa em um único programa poderia travar o sistema inteiro, corromper dados de outros processos ou comprometer a segurança da máquina. Restringir o acesso direto ao modo kernel garante isolamento, estabilidade e segurança — o SO atua como um "porteiro" que valida e intermedia cada solicitação.

### 2.4 Processos

Durante a instalação do Windows, vários processos são executados, cada um responsável por uma parte do trabalho:

- **`setup.exe`** — processo principal do instalador, coordena todas as etapas (particionamento, cópia, configuração).
- **`WinPE` (Windows Preinstallation Environment)** — ambiente mínimo em que o instalador roda antes de haver um Windows completo instalado.
- **Processos de cópia/expansão de arquivos** — responsáveis por transferir e descompactar os arquivos do sistema para a unidade de destino.
- **`services.exe` e processos de rede** — iniciados na etapa de configuração inicial, responsáveis por Plug-and-Play, rede e demais serviços de segundo plano.

**O que caracteriza um processo:** um processo é um programa em execução, com seu próprio espaço de memória, estado (registradores, contador de programa), prioridade de execução e recursos alocados (arquivos abertos, handles) — diferente do programa, que é apenas o código armazenado em disco.

**Recursos que os processos precisam:** memória RAM, tempo de CPU, acesso ao disco de destino e, em alguns casos, acesso à rede (para baixar atualizações durante a instalação).

**Como o SO gerencia esses processos:** o kernel mantém uma tabela de processos, controla o escalonamento (quem usa a CPU e quando), isola o espaço de memória de cada processo e libera os recursos quando o processo termina.

### 2.5 Programa × Processo × Thread

**Exemplo:** o programa responsável pela cópia e expansão dos arquivos do Windows durante a instalação.

- **Programa:** o executável do instalador (ex.: o módulo de cópia de arquivos dentro do `setup.exe`), armazenado como código estático na mídia de instalação — nesse estado, é apenas um arquivo, sem estar em execução.
- **Processo:** quando o instalador inicia a etapa de "Cópia dos arquivos", o sistema operacional carrega esse programa na memória, cria um processo para ele, com seu próprio espaço de endereçamento e recursos — a partir daí ele passa a consumir CPU e memória ativamente.
- **Thread:** dentro desse processo, podem existir múltiplas threads (linhas de execução) — por exemplo, uma thread copiando um grupo de arquivos enquanto outra thread verifica a integridade de arquivos já copiados, ou atualiza a barra de progresso na tela.

**Por que usar múltiplas threads pode ser útil:** threads compartilham a mesma memória do processo, então é mais leve criar e alternar entre elas do que entre processos separados. Isso permite paralelizar tarefas (como copiar vários arquivos simultaneamente) e manter a interface responsiva (uma thread atualiza a barra de progresso enquanto outra continua copiando dados), reduzindo o tempo total da instalação.

### 2.6 Sistema de Arquivos

O sistema de arquivos é responsável por organizar como os dados são armazenados e localizados na unidade de destino.

- **O que acontece com os dados existentes:** se a unidade já possuía dados de uma instalação anterior, eles são marcados como não referenciados (no caso da formatação) ou completamente sobrescritos (se houver formatação de baixo nível), tornando-os inacessíveis pelo sistema de arquivos.
- **Formatação da unidade:** cria as estruturas lógicas do sistema de arquivos escolhido — no caso do Windows, tipicamente o **NTFS** — como a Master File Table (MFT), tabelas de alocação e metadados de permissão.
- **Criação/organização das estruturas necessárias:** são criadas as pastas padrão do Windows (`Windows`, `Program Files`, `Users`) e as estruturas de journaling do NTFS, que ajudam a manter a integridade em caso de falhas.
- **Cópia dos arquivos de instalação:** o conteúdo da imagem do Windows (`install.wim`/`install.esd`) é expandido diretamente na estrutura NTFS recém-criada.
- **Criação dos arquivos necessários para inicialização:** são gravados os arquivos de boot (`bootmgr`, pasta `Boot`, `BCD`) na partição EFI/de sistema, permitindo que o firmware localize o carregador do Windows nas próximas inicializações.
- **Organização dos arquivos após a instalação:** o sistema de arquivos passa a manter, de forma contínua, os arquivos de sistema, os perfis de usuário, o registro do Windows e os programas instalados, todos localizáveis por meio de suas estruturas de indexação.

**Diferenciando os três conceitos:**
- **Apagar dados** — remover a referência a um ou mais arquivos específicos do sistema de arquivos (o conteúdo pode continuar fisicamente no disco até ser sobrescrito).
- **Particionar uma unidade** — dividir o disco físico em áreas lógicas independentes (partições), cada uma podendo ter seu próprio sistema de arquivos; não implica, por si só, remover ou organizar arquivos.
- **Formatar um sistema de arquivos** — criar (ou recriar) as estruturas lógicas de organização de dados dentro de uma partição, tornando-a utilizável por um sistema operacional; normalmente invalida o acesso aos dados anteriores daquela partição.

### 2.7 Entrada/Saída e Drivers de Dispositivos

**Dispositivos de E/S envolvidos no processo:** teclado e mouse (interação com o instalador), monitor (exibição das telas de instalação), unidade de instalação/pendrive (leitura dos arquivos do Windows), SSD/HD de destino (gravação do sistema), rede (opcional, para baixar atualizações durante a instalação) e, após a instalação, dispositivos de áudio e demais periféricos.

**Como o Windows se comunica com esses dispositivos:** o Gerenciador de Entrada/Saída do kernel recebe as solicitações de acesso a um dispositivo (por exemplo, "ler um setor do disco") e as encaminha ao driver correspondente, que traduz esse pedido genérico em comandos específicos entendidos pelo controlador daquele hardware.

**Papel dos drivers e sua importância:**
- **Durante a instalação:** drivers básicos genéricos (incluídos no próprio instalador) permitem que o sistema reconheça e utilize teclado, mouse, monitor, controlador de disco e, muitas vezes, adaptadores de rede, mesmo sem ainda haver um driver específico do fabricante instalado.
- **Depois da instalação:** drivers mais específicos e otimizados (de placa de vídeo, chipset, Wi-Fi, áudio) são instalados para que o hardware funcione com desempenho total e todos os recursos disponíveis — sem eles, dispositivos podem funcionar de forma limitada (ex.: resolução de vídeo básica) ou não funcionar (ex.: Wi-Fi ausente até o driver ser instalado).

Sem drivers, o kernel do Windows saberia *que* existe um disco ou uma placa de vídeo, mas não *como* se comunicar com aquele modelo específico — os drivers são a camada de tradução que viabiliza o uso real do hardware.

---

## 3. Linha do Tempo da Instalação do Windows

| Etapa | O que acontece? | Conceito envolvido | Por que é importante? |
|---|---|---|---|
| **1. Inicialização** | O computador é ligado; o firmware (BIOS/UEFI) realiza o POST e assume o controle inicial da máquina, antes de qualquer sistema operacional estar carregado. | Modos de execução (o firmware ainda não distingue modo usuário/kernel — atua em nível mais baixo que o SO) | Sem essa etapa, nenhum software, incluindo o instalador, poderia sequer começar a ser carregado. |
| **2. Inicialização do instalador** | O firmware lê a mídia de instalação e carrega o Windows PE (mini sistema com kernel reduzido) na memória RAM. | Kernel; Processos | É o kernel do WinPE que passa a gerenciar CPU e memória a partir daqui, permitindo que o instalador (`setup.exe`) rode como processo. |
| **3. Reconhecimento do hardware** | O instalador identifica os dispositivos disponíveis (discos, controladores, rede) usando drivers básicos incluídos na mídia. | Entrada/Saída; Drivers de dispositivo | Sem reconhecer o hardware, o instalador não saberia em qual unidade instalar o sistema nem conseguiria receber comandos do teclado/mouse. |
| **4. Seleção da unidade** | O usuário escolhe em qual disco/partição o Windows será instalado. | Componentes do SO (Gerenciador de E/S) | Define onde as próximas operações de particionamento, formatação e cópia serão realizadas. |
| **5. Particionamento/formatação** | O disco é dividido em partições (ex.: EFI, sistema) e a partição de destino é formatada com o sistema de arquivos NTFS. | Sistema de arquivos | Cria a estrutura lógica necessária para que arquivos possam ser gravados, localizados e organizados no disco. |
| **6. Cópia dos arquivos** | Os arquivos da imagem do Windows são copiados e expandidos para a partição recém-formatada, com múltiplas threads trabalhando em paralelo. | Processo × Programa × Thread | O uso de múltiplas threads acelera a cópia e mantém a interface do instalador responsiva durante a operação. |
| **7. Instalação do Windows** | São gravados os arquivos de sistema, o bootloader e as estruturas de registro; o computador reinicia para concluir a instalação a partir do disco interno. | Kernel; Sistema de arquivos | É nesse ponto que o kernel definitivo do Windows passa a estar presente no disco e pronto para ser carregado. |
| **8. Instalação/configuração de drivers** | Drivers básicos e, posteriormente, drivers específicos do fabricante são carregados para os dispositivos detectados. | Entrada/Saída; Drivers de dispositivo | Garante que todo o hardware (vídeo, rede, áudio) funcione corretamente e com desempenho pleno. |
| **9. Inicialização do sistema** | O bootloader localiza e carrega o kernel definitivo do Windows a partir do disco; serviços do sistema são iniciados. | Kernel; Modos de execução | Marca a transição definitiva do ambiente temporário do instalador para o sistema operacional completo, agora operando em modo kernel/usuário de forma permanente. |
| **10. Windows pronto para utilização** | O usuário configura conta, rede e preferências; o sistema está pronto para executar aplicações. | Componentes do SO; Processos | Representa o momento em que a máquina deixa de ser apenas hardware controlado por um instalador temporário e passa a ser um sistema completo, multiusuário e multiprocesso. |

---

## 4. Desafio Final

### 4.1 Se não existisse um Sistema Operacional, o que precisaria ser feito diretamente pelo usuário/programas?

Sem um SO, cada programa precisaria conter, dentro do próprio código, toda a lógica de baixo nível hoje delegada ao sistema: gerenciar diretamente a alocação de memória física (sem proteção entre programas), controlar os registradores e o escalonamento da CPU manualmente, implementar do zero a comunicação com cada modelo específico de disco, teclado, monitor e placa de rede (sem uma camada de drivers padronizada), e criar sua própria forma de organizar dados no disco (sem um sistema de arquivos comum, cada programa "inventaria" sua própria estrutura de armazenamento). Também não haveria isolamento entre programas — um erro em um software poderia sobrescrever a memória de outro ou travar a máquina inteira, já que não existiria um kernel mediando o acesso ao hardware em modo privilegiado.

### 4.2 Qual conceito é mais importante para transformar hardware em um sistema capaz de executar aplicações?

O **kernel** é o conceito mais determinante nesse processo. É ele quem primeiro assume o controle da máquina após o boot, sendo responsável por inicializar e gerenciar todos os demais recursos — memória, processos, sistema de arquivos e dispositivos de E/S por meio dos drivers. Todos os outros conceitos estudados (modos de execução, processos, threads, sistema de arquivos, drivers) existem e funcionam *porque* o kernel os coordena e os protege: é ele que impõe a separação entre modo usuário e modo kernel, que decide o escalonamento dos processos, que intermedeia o acesso aos drivers e que garante a integridade do sistema de arquivos. Sem o kernel, os demais componentes seriam apenas peças soltas, sem nenhuma camada central para orquestrá-los — por isso ele é o elemento que efetivamente transforma um conjunto de componentes de hardware em um sistema operacional funcional, capaz de executar aplicações de forma segura e organizada.
