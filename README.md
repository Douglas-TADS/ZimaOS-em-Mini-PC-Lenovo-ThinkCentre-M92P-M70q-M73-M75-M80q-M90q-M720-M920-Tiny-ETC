# Correção do erro 1962 após instalar o ZimaOS em Lenovo ThinkCentre

Este tutorial apresenta um procedimento para corrigir o **erro 1962** que pode ocorrer durante a inicialização de alguns mini PCs Lenovo ThinkCentre após a instalação do ZimaOS.

O procedimento foi utilizado como referência nos modelos Lenovo ThinkCentre **M92p, M70q, M73, M75, M80q, M90q, M720, M920 e outros modelos da linha Tiny**. A compatibilidade pode variar conforme o modelo, a versão do firmware/BIOS e a configuração de armazenamento.

## 1. Instale o ZimaOS

Primeiro, faça a instalação do ZimaOS seguindo as instruções oficiais do desenvolvedor:

[Documentação oficial — Como instalar o ZimaOS](https://www.zimaspace.com/docs/pt-PT/zimaos/how-to-install-zimaos)

Conclua o procedimento de instalação até o passo 4.

**Problema:** após finalizar a instalação e reiniciar o computador, pode ocorrer o erro **1962**, impedindo a inicialização normal do ZimaOS.

## 2. Crie um pendrive do Boot Repair Disk

Baixe a imagem do Boot Repair Disk:

[Download do Boot Repair Disk — SourceForge](https://sourceforge.net/projects/boot-repair-cd/)

Grave a imagem em um pendrive inicializável, da mesma maneira utilizada para criar o pendrive de instalação do ZimaOS.

Conecte o pendrive ao Lenovo ThinkCentre e ligue o computador inicializando por ele. Aguarde o carregamento do Boot Repair Disk.

## 3. Abra o terminal e identifique o disco

Abra o terminal no ambiente do Boot Repair Disk e execute:

```bash
sudo fdisk -l
```

Identifique o disco em que o ZimaOS foi instalado e sua partição EFI.

**Atenção:** os comandos deste tutorial usam `/dev/sda` como exemplo de disco e `/dev/sda1` como exemplo de partição EFI. Se o seu computador apresentar identificadores diferentes, substitua-os nos comandos seguintes pelos dispositivos corretos. Não escolha uma partição apenas pelo número: confirme sua identificação na saída do `fdisk -l`.

## 4. Monte a partição EFI

Crie o diretório de montagem:

```bash
sudo mkdir -p /mnt/efi
```

Monte a partição EFI (no exemplo, `/dev/sda1`):

```bash
sudo mount /dev/sda1 /mnt/efi
```

## 5. Verifique as entradas de inicialização UEFI

Execute:

```bash
sudo efibootmgr -v
```

Esse comando exibe as entradas de inicialização UEFI existentes, seus identificadores e a ordem de inicialização.

## 6. Crie uma entrada de inicialização para o ZimaOS

Execute o comando abaixo, considerando o disco e a partição EFI do exemplo:

```bash
sudo efibootmgr -c -d /dev/sda -p 1 -L "ZimaOS" -l '\EFI\BOOT\bootx64.efi'
```

O comando cria uma nova entrada UEFI com o nome **ZimaOS**, apontando para o carregador `bootx64.efi` na partição EFI indicada.

## 7. Confira se a entrada foi criada e a ordem de boot

Execute:

```bash
sudo efibootmgr
```

Procure uma entrada semelhante a:

```text
Boot0000* ZimaOS
```

O número pode ser diferente de `0000`. O asterisco indica que a entrada está ativa.

**Importante:** para confirmar se o ZimaOS está configurado para iniciar primeiro, confira também a linha `BootOrder`. O identificador da entrada ZimaOS deve aparecer na primeira posição. Se a entrada existir, mas não estiver em primeiro lugar, será necessário ajustar a ordem usando os identificadores exibidos pelo seu próprio computador. Não copie números de exemplo.

## 8. Reinicie o computador

Se a entrada UEFI foi criada corretamente e a ordem de inicialização está adequada:

1. Desligue ou reinicie o computador.
2. Remova o pendrive do Boot Repair Disk.
3. Ligue o Lenovo ThinkCentre.

O ZimaOS deverá iniciar normalmente.

## Observações

- Os nomes dos discos e das partições podem variar. Confira cuidadosamente a saída de `sudo fdisk -l` antes de executar os comandos.
- Este procedimento altera as entradas de inicialização UEFI. Execute-o somente depois de identificar corretamente o disco e a partição EFI.
- Se o erro persistir, confira se o firmware está configurado para inicialização UEFI e se o caminho do carregador EFI utilizado no comando realmente existe na partição EFI.
- Este tutorial documenta um procedimento de recuperação específico; não substitui a documentação oficial de instalação do ZimaOS.

---

**Projeto:** ZimaOS em mini PCs Lenovo ThinkCentre  
**Objetivo:** documentar a solução do erro 1962 após a instalação do ZimaOS.
