<!-- LOGOTIPO DO PROJETO -->
<div style="display: flex; justify-content: center;">
   <a href="https://github.com/SEU-USUARIO/SEU-PROJETO">
     <img src="docs/figures/logo.png" alt="Logo" width="200" height="100">
   </a>
</div>

<h3 align="center">smartmontools</h3>

<div style="display: flex; justify-content: center;">
  <a href="https://doi.org/SEU-DOI">
    <img src="https://zenodo.org/badge/SEU_BADGE.svg" alt="DOI">
  </a>
</div>

<p align="center">
 Um guia prático para instalar e usar o smartmontools no Linux Ubuntu.
 <br />
 <a href="https://github.com/SEU-USUARIO/SEU-PROJETO"><strong>Explore os documentos »</strong></a>
 <br />
 <br />
 <a href="https://github.com/SEU-USUARIO/SEU-PROJETO">Ver demonstração</a>
 ·
 <a href="https://github.com/SEU-USUARIO/SEU-PROJETO">Relatar bug</a>
 ·
 <a href="https://github.com/SEU-USUARIO/SEU-PROJETO">Solicitar recurso</a>
</p>


## Resumo

Guia direto para instalar, verificar e usar o smartmontools para monitorar a saúde de discos (SMART) no Linux Ubuntu.

## _Abstract_

_A straightforward guide to installing, verifying, and using smartmontools to monitor disk health (SMART) on Linux Ubuntu._

## Descrição

### `smartmontools`

O `smartmontools` é o pacote principal que reúne ferramentas para monitorar a saúde de discos rígidos e SSDs usando o `S.M.A.R.T.`. Ele inclui utilitários de linha de comando e um serviço de monitoramento.

### `smartctl`

O `smartctl` é o utilitário de linha de comando do `smartmontools` usado para consultar atributos SMART, executar testes e gerar relatórios detalhados dos discos.

### `smartd`

O `smartd` é o serviço em segundo plano do `smartmontools` que monitora os discos continuamente e pode emitir alertas conforme a configuração.


  

## Descrição

`smartmontools`

`smartctl`

`smartd`

<!-- COMEÇANDO -->
### Começando

Este documento descreve a instalação e o uso básico do smartmontools em ambientes Linux Ubuntu.

### Pré-requisitos

- Acesso ao `Terminal Emulator`
- Permissão de `sudo`
- Conexão com a internet para instalar pacotes via `apt`

* [![Ubuntu](https://img.shields.io/badge/Ubuntu-20.04+-E95420?style=flat-square&logo=ubuntu&logoColor=white)](https://ubuntu.com/)

* [![APT](https://img.shields.io/badge/APT-apt-0A7CC1?style=flat-square)](https://manpages.ubuntu.com/manpages/jammy/en/man8/apt.8.html)

* [![SMART](https://img.shields.io/badge/SMART-monitoring-2E7D32?style=flat-square)](https://www.smartmontools.org/)

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>


## Guia de instalação

### Instalar o smartmontools (Ubuntu)

Para instalar o smartmontools, siga os passos abaixo:

1. Abra o `Terminal Emulator`. Você pode fazer isso pressionando:

    ```bash
    Ctrl + Alt + T
    ```

2. Certifique-se de que seu sistema esteja limpo e atualizado.

    2.1 Limpar o `cache` do gerenciador de pacotes `apt`. Especificamente, ele remove todos os arquivos de pacotes (`.deb`) baixados pelo `apt` e armazenados em `/var/cache/apt/archives/`. Digite o seguinte comando:
    ```bash
    sudo apt clean
    ```

    2.2 Remover pacotes `.deb` antigos ou duplicados do `cache` local. É útil para liberar espaço, pois remove apenas os pacotes que não podem mais ser baixados (ou seja, versões antigas de pacotes que foram atualizados). Digite o seguinte comando:
    ```bash
    sudo apt autoclean
    ```

    2.3 Remover pacotes que foram automaticamente instalados para satisfazer as dependências de outros pacotes e que não são mais necessários. Digite o seguinte comando:
    ```bash
    sudo apt autoremove -y
    ```

    2.4 Buscar as atualizações disponíveis para os pacotes que estão instalados em seu sistema. Digite o seguinte comando e pressione `Enter`:
    ```bash
    sudo apt update
    ```

    2.5 **Corrigir pacotes quebrados**: Isso atualizará a lista de pacotes disponíveis e tentará corrigir pacotes quebrados ou com dependências ausentes:
    ```bash
    sudo apt --fix-broken install
    ```

    2.6 Limpar o `cache` do gerenciador de pacotes `apt` novamente:
    ```bash
    sudo apt clean
    ```

    2.7 Para ver a lista de pacotes a serem atualizados, digite o seguinte comando e pressione `Enter`:
    ```bash
    sudo apt list --upgradable
    ```

    2.8 Realmente atualizar os pacotes instalados para as suas versões mais recentes, com base na última vez que você executou `sudo apt update`. Digite o seguinte comando e pressione `Enter`:
    ```bash
    sudo apt full-upgrade -y
    ```

3. Instale o pacote `smartmontools`:
    ```bash
    sudo apt install smartmontools -y
    ```

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

## Guia de instalação

### Verificar instalação e habilitar o smartd

1. Verifique a versão instalada:

```bash
smartctl --version
```

2. (Opcional) Habilite o serviço `smartd` para monitoramento em segundo plano:

```bash
sudo systemctl enable --now smartd
```

3. Verifique o status do serviço:

```bash
systemctl status smartd
```

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

#### `Windows` [2]

Se você precisar usar o smartmontools no Windows, instale o pacote pelo instalador oficial e execute o `smartctl` no Prompt de Comando ou PowerShell.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

### Atualizar índices do sistema [3]

Exemplo simples para garantir que o `apt` está atualizado antes de instalar pacotes:

1. `sudo apt update`
2. `sudo apt full-upgrade -y`
3. `sudo apt autoremove -y`

### Instalar o smartmontools via `apt`

#### `Linux`

1. **Instale o pacote:**

  - **Pelo terminal:** `sudo apt install smartmontools -y`

  <p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

#### `Windows`

1. **Instale o pacote:**

  - **Pelo instalador oficial** e verifique com `smartctl --version`

  <p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

## Como executar a aplicação

### Executar a partir do `Terminal Emulator`

1. Liste os discos disponíveis:

```bash
lsblk
```

2. Consulte o SMART do disco desejado (exemplo com `/dev/sda`):

```bash
sudo smartctl -a /dev/sda
```

3. Inicie um teste curto de saúde:

```bash
sudo smartctl -t short /dev/sda
```

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>


### Executar a partir da `Graphical User Interface (GUI)`

O smartmontools não possui GUI oficial. Use o `smartctl` via terminal ou habilite o `smartd` para monitoramento automático.

## Mostrar ajuda

1. Mostre a ajuda do `smartctl`:

```bash
smartctl --help
```

### Exemplo de Saída Esperada

```bash
smartctl 7.x (build info)
usage: smartctl [options] device
```


## O que o aplicativo faz?

O smartmontools permite monitorar a saúde de discos rígidos e SSDs por meio do SMART, executando testes e exibindo relatórios.

- Lê os atributos SMART do disco
- Executa auto-testes (curto e longo)
- Exibe logs de erros e testes anteriores


## O que o aplicativo exibe como saída(s)

# Relatório SMART do Disco

## 1. Identificação do Dispositivo

- Modelo, número de série e firmware.
- Capacidade e tipo de interface (SATA, NVMe).

## 2. Estado Geral de Saúde

- SMART overall-health self-assessment.
- Indicação de falhas iminentes.

## 3. Atributos SMART

- Lista de atributos críticos (reallocated, pending, temperature).
- Valores atuais, pior valor e limiares.

## 4. Logs de Erros

- Erros registrados e contagem.
- Últimos eventos relevantes.

## 5. Logs de Testes

- Histórico de auto-testes executados.
- Resultados e tempo de execução.

## 6. Observações Operacionais

- Indicação de necessidade de backup.
- Recomendações de monitoramento.


## Saídas Essenciais no Relatório

- Tabela de atributos SMART
- Status geral de saúde
- Resultado do último auto-teste
- Temperatura do disco

## 1. Função da Aplicação

Monitorar a saúde do disco e fornecer sinais de risco antecipado.

### 1.1 Entrada(s)

1. Dispositivos de bloco (ex.: `/dev/sda`, `/dev/nvme0n1`).

### 1.2 Saída(s)

1. Relatório detalhado do SMART via `smartctl`.

## 2. Observação(ões)

1. Execute comandos com `sudo` para acesso completo ao SMART.
2. Em ambientes com múltiplos discos, verifique o dispositivo correto com `lsblk`.

# 3. Futura(s) Melhoria(s)

- Automatizar alertas por e-mail com `smartd`.
- Integrar relatórios com ferramentas de inventário.

<!-- LICENÇA -->
## Licença

Distribuído sob a licença `MIT`. Consulte `LICENSE.txt` para obter mais informações.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

<!-- ROTEIRO -->
## Roteiro

- [ ] Adicionar exemplos de saída reais do `smartctl`
- [ ] Incluir guia rápido de interpretação dos atributos SMART
- [ ] Incluir seção de troubleshooting
- [ ] Suporte multilíngue

Consulte os problemas abertos para obter uma lista completa dos recursos propostos.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>


<!-- CONTRIBUIÇÔES -->
## Contribuições

Explique como contribuir (fork, branch, PR, issues).

1. Bifurque o projeto
2. Crie sua ramificação (`git checkout -b feature/NovaFuncionalidade`)
3. Confirme suas alterações (`git commit -m 'Describe change'`)
4. Envie para a filial (`git push origin feature/NovaFuncionalidade`)
5. Abra uma solicitação `pull`

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>


<!-- ACKNOWLEDGMENTS -->
## Agradecimentos

* [Best README Template](https://github.com/othneildrew/Best-README-Template?tab=readme-ov-file)

* [Choose an Open Source License](https://choosealicense.com)

* [GitHub Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet)

* [Malven's Flexbox Cheatsheet](https://flexbox.malven.co/)

* [Malven's Grid Cheatsheet](https://grid.malven.co/)

* [Img Shields](https://shields.io)

* [GitHub Pages](https://pages.github.com)

* [Font Awesome](https://fontawesome.com)

* [React Icons](https://react-icons.github.io/react-icons/search)

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>


## Referências

[1] OPENAI. ***Instalar***. Disponível em: <https://chatgpt.com/g/g-p-6980caf949648191ad6acfcdbe590f9e-instalar/c/697ae047-9900-8326-b1e9-c5f1634b0df2>. ChatGPT. Acessado em: 12/02/2026.
[2] SMARTMONTOOLS. ***smartmontools***. Disponível em: <https://www.smartmontools.org/>. Acessado em: 12/02/2026.
[3] UBUNTU. ***apt***. Disponível em: <https://manpages.ubuntu.com/manpages/jammy/en/man8/apt.8.html>. Acessado em: 12/02/2026.

