[manual-funcionalidades-ubuntu (2).md](https://github.com/user-attachments/files/31712624/manual-funcionalidades-ubuntu.2.md)
<p align="center">
  <img src="./banner-ubuntu-manual.svg" alt="Manual: Funcionalidades do Ubuntu que o Windows não tem" width="100%"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Sistema-Ubuntu%20Linux-3B0764?style=for-the-badge&logo=ubuntu&logoColor=E9D5FF" alt="Ubuntu"/>
  <img src="https://img.shields.io/badge/Compara%C3%A7%C3%A3o-Windows-0B0210?style=for-the-badge&logoColor=D8B4FE" alt="Windows"/>
  <img src="https://img.shields.io/badge/Fun%C3%A7%C3%B5es-6-A855F7?style=for-the-badge&logoColor=white" alt="6 funções"/>
</p>

# Manual: Funcionalidades do Ubuntu que não existem no Windows

## Introdução

Este manual apresenta 6 funcionalidades simples do Ubuntu (Linux) que não existem, ou funcionam de forma bem diferente, no Windows. O objetivo é que qualquer pessoa curiosa consiga testar cada uma delas rapidamente em uma máquina virtual com Ubuntu.

---

## <img src="https://img.shields.io/badge/01-3B0764?style=flat-square" valign="middle"/> Gerenciador de pacotes central (APT)

No Windows, cada programa é baixado de um site diferente, em formato `.exe`, e cada um tem seu próprio instalador. No Ubuntu, quase todo software vem de repositórios centrais, gerenciados por um único comando.

**Como testar:**

```bash
sudo apt update
sudo apt list --upgradable
sudo apt install htop
```

O primeiro comando atualiza a lista de pacotes disponíveis. O segundo mostra todos os programas do sistema com atualização pendente, de uma vez só. O terceiro instala o programa `htop` (um monitor de sistema) já resolvendo automaticamente qualquer dependência necessária.

Para remover: `sudo apt remove htop`

> 🟣 **Por que importa:** não existe download de site em site — tudo vem de um repositório confiável e centralizado.

---

## <img src="https://img.shields.io/badge/02-3B0764?style=flat-square" valign="middle"/> Modelo de superusuário com `sudo`

No Windows, uma conta "Administrador" já tem os privilégios liberados o tempo todo (com uma confirmação pontual do UAC). No Linux, existe um usuário separado chamado **root**, e o usuário comum só ganha privilégios administrativos comando a comando, usando `sudo`.

**Como testar:**

```bash
whoami
sudo whoami
```

O primeiro comando mostra seu usuário normal. O segundo, com `sudo`, pede sua senha e mostra `root` — provando que, só naquele comando, você virou o superusuário do sistema.

> 🟣 **Por que importa:** cada ação administrativa exige autorização explícita, comando por comando.

---

## <img src="https://img.shields.io/badge/03-3B0764?style=flat-square" valign="middle"/> Filosofia "tudo é um arquivo"

No Ubuntu, até informações de hardware e processos em execução podem ser lidas como se fossem arquivos de texto comuns. Isso não existe no Windows.

**Como testar:**

```bash
cat /proc/cpuinfo
ls /dev
```

O primeiro comando mostra os detalhes do processador do computador, lidos diretamente de um "arquivo" do sistema. O segundo lista os dispositivos conectados (discos, portas USB etc.), também representados como arquivos dentro da pasta `/dev`.

> 🟣 **Por que importa:** hardware, processos e até a memória aparecem como arquivos dentro do sistema.

---

## <img src="https://img.shields.io/badge/04-3B0764?style=flat-square" valign="middle"/> Sistema de arquivos sensível a maiúsculas e minúsculas

No Windows (NTFS padrão), `arquivo.txt` e `Arquivo.txt` são tratados como o mesmo arquivo. No Ubuntu, são dois arquivos completamente diferentes.

**Como testar:**

```bash
touch teste.txt Teste.txt
ls
```

O comando `ls` vai mostrar os dois arquivos lado a lado, provando que o sistema diferencia letras maiúsculas de minúsculas no nome.

> 🟣 **Por que importa:** o sistema distingue letras maiúsculas de minúsculas em qualquer nome de arquivo.

---

## <img src="https://img.shields.io/badge/05-3B0764?style=flat-square" valign="middle"/> Agendamento de tarefas nativo com `cron`

O Windows precisa do "Agendador de Tarefas", um programa à parte com interface gráfica. No Ubuntu, o agendamento de tarefas (`cron`) já vem embutido no sistema desde sempre, e pode ser configurado só por linha de comando.

**Como testar:**

```bash
crontab -e
```

Ao abrir o editor, adicione a linha abaixo para, por exemplo, criar um arquivo todo dia às 8h da manhã:

```
0 8 * * * touch /home/$USER/lembrete.txt
```

Salve e feche o editor. A tarefa já fica agendada no sistema, sem precisar de nenhum programa extra.

> 🟣 **Por que importa:** agendamento nativo do sistema, sem instalar nenhum programa extra.

---

## <img src="https://img.shields.io/badge/06-3B0764?style=flat-square" valign="middle"/> Páginas de manual (`man`) para qualquer comando

No Windows, a documentação de um comando costuma exigir uma busca no navegador. No Ubuntu, praticamente todo comando do sistema já vem com um manual completo embutido, acessível offline, direto no terminal.

**Como testar:**

```bash
man ls
```

Isso abre o manual completo do comando `ls`, explicando todas as suas opções (como `-l`, `-a`, `-h`). Use as setas para navegar e a tecla `q` para sair. Funciona da mesma forma para praticamente qualquer comando, por exemplo `man cp` ou `man chmod`.

> 🟣 **Por que importa:** documentação completa e offline para quase qualquer comando do sistema.

---

## Conclusão

Essas 6 funcionalidades mostram como o Ubuntu tem uma filosofia diferente do Windows: mais centrada em terminal, em arquivos de texto simples e em ferramentas nativas do sistema, ao invés de programas gráficos separados para cada tarefa. Todas podem ser testadas em poucos minutos em uma máquina virtual.

<p align="center"><sub>🖤 Manual produzido para a Tarefa 05 — Virtualização e Sistemas Operacionais</sub></p>
