# Manual: Funcionalidades do Ubuntu que não existem no Windows

## Introdução

Este manual apresenta 5 funcionalidades simples do Ubuntu (Linux) que não existem, ou funcionam de forma bem diferente, no Windows. O objetivo é que qualquer pessoa curiosa consiga testar cada uma delas rapidamente em uma máquina virtual com Ubuntu.

---

## 1. Gerenciador de pacotes central (APT)

No Windows, cada programa é baixado de um site diferente, em formato `.exe`, e cada um tem seu próprio instalador. No Ubuntu, quase todo software vem de repositórios centrais, gerenciados por um único comando.

**Como testar:**

```bash
sudo apt update
sudo apt list --upgradable
sudo apt install htop
```

O primeiro comando atualiza a lista de pacotes disponíveis. O segundo mostra todos os programas do sistema com atualização pendente, de uma vez só. O terceiro instala o programa `htop` (um monitor de sistema) já resolvendo automaticamente qualquer dependência necessária.

Para remover: `sudo apt remove htop`

---

## 2. Modelo de superusuário com `sudo`

No Windows, uma conta "Administrador" já tem os privilégios liberados o tempo todo (com uma confirmação pontual do UAC). No Linux, existe um usuário separado chamado **root**, e o usuário comum só ganha privilégios administrativos comando a comando, usando `sudo`.

**Como testar:**

```bash
whoami
sudo whoami
```

O primeiro comando mostra seu usuário normal. O segundo, com `sudo`, pede sua senha e mostra `root` — provando que, só naquele comando, você virou o superusuário do sistema.

---

## 3. Filosofia "tudo é um arquivo"

No Ubuntu, até informações de hardware e processos em execução podem ser lidas como se fossem arquivos de texto comuns. Isso não existe no Windows.

**Como testar:**

```bash
cat /proc/cpuinfo
ls /dev
```

O primeiro comando mostra os detalhes do processador do computador, lidos diretamente de um "arquivo" do sistema. O segundo lista os dispositivos conectados (discos, portas USB etc.), também representados como arquivos dentro da pasta `/dev`.

---

## 4. Sistema de arquivos sensível a maiúsculas e minúsculas

No Windows (NTFS padrão), `arquivo.txt` e `Arquivo.txt` são tratados como o mesmo arquivo. No Ubuntu, são dois arquivos completamente diferentes.

**Como testar:**

```bash
touch teste.txt Teste.txt
ls
```

O comando `ls` vai mostrar os dois arquivos lado a lado, provando que o sistema diferencia letras maiúsculas de minúsculas no nome.

---

## 5. Agendamento de tarefas nativo com `cron`

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

---

## Conclusão

Essas 5 funcionalidades mostram como o Ubuntu tem uma filosofia diferente do Windows: mais centrada em terminal, em arquivos de texto simples e em ferramentas nativas do sistema, ao invés de programas gráficos separados para cada tarefa. Todas podem ser testadas em poucos minutos em uma máquina virtual.
