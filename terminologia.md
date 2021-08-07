# Terminology

## macOS
OS baseado no UNIX, proprietáro da Apple, usedo para as máquinas Mac "É o que faz um Mac um Mac".

## Windows
OS da Microsoft que tem um suporte para um grande grupo de dispositivos (fique com este sistema operacional
se você não quiser dores de cabeça)

## Linux
Família de sistemas operacionais de código aberto semelhantes ao Unix baseados no kernel Linux, um kernel de sistema
operacional lançado pela primeira vez em 17 de setembro de 1991, por Linus Torvalds. O Linux normalmente é empacotado em uma
distribuição Linux.
Observe que, embora o macOS e o Linux possam ser baseados em UNIX, eles são imensamente diferentes. 

## Distros
As distros Linux são como o Linux é distribuído. No entanto, quando se trata de macOS, as distribuições são
instaladores macOS mistos com um monte de ferramentas que não são da Apple. Não use distros do macOS.

## Hackintosh 
O processo de instalação do macOS em um PC, observe que Hackintosh NÃO É o SO, também pode se referir à
máquina que foi "hackeada" para que o macOS fosse executado. 

```
EX .: instalei o macOS nesta máquina Windows, portanto tenho um Hackintosh. Mas eu NÃO instalei o "Hackintosh".
```

## Bootloader
Software que carrega um sistema operacional, geralmente feito pelos criadores do sistema operacional. O
OpenCore não é tecnicamente um bootloader per se (veja a explicação do gerenciador de boot abaixo). 
O Boot.efi da Apple seria o loader de boot real em um Mac ou Hackintosh.

## Boot Manager
Software que gerencia bootloaders - temos muitos deles: Clover, systemd-boot, OpenCore, rEFInd, rEFIt

## OpenCore
O novo hotness no cenário Hackintosh, feito com a segurança em mente pelo Dortania tem boot mais rápido e mais leve
do que o Clover. É muito mais trabalhoso configurar, mas também suporta muitas coisas muito mais nativamente do que o Clover
(como Hibernação, FileVault 2, Boot HotKeys ...).

## Clover
Um bootloader agora considerado legado com o lançamento do OpenCore. Este guia não cobrirá os usos de
este software.

## ACPI
A configuração avançada e interface de energia (ACPI) fornece um padrão aberto que os sistemas operacionais podem usar para descobrir e configurar componentes de hardware do computador, mais sobre isso será discutido posteriormente no guia.

## DSDT/SSDT
Tabelas em sua ACPI que descrevem os dispositivos e como o sistema operacional deve interagir com eles, por exemplo colocando o
PC em hibernação, wake, alternar GPUs, portas USB etc.

## .AML
O formato de arquivo compilado do ACPI e o que seu PC executará. 
.DAT é outra extensão com exatamente o mesmo uso.

## .DSL
O código-fonte da ACPI, é o que você edita e compila para o seu computador. NÃO
misture este formato de arquivo com .ASL.

## Kexts
Também conhecidos como extensões de kernel, são drivers do macOS. Eles estão acostumados a
executar tarefas diferentes, como drivers de dispositivo ou para uma finalidade diferente (no Hackintoshing), como corrigir o
SO, injetando informações ou executando tarefas. Kexts não são a única parte de um bom Hackintosh, pois eles são
comumente emparelhado com patches e correções ACPI.

## BIOS
O sistema básico de entrada / saída é o firmware usado para realizar a inicialização do hardware durante o processo de inicialização
(inicialização ao ligar) e para fornecer serviços de tempo de execução para sistemas operacionais e programas. O firmware do BIOS
vem pré-instalado na placa de sistema de um computador pessoal e é o primeiro software a ser executado quando ligado
(fonte: Wikipedia). É um software legado que foi feito na década de 70 e ainda é usado para isso
dia devido ao seu vencimento.

## UEFI
The Unified Extensible Firmware Interface (UEFI) is a specification that defines a software interface
between an operating system and platform firmware. UEFI replaces the legacy Basic Input/Output System (BIOS)
firmware interface originally present in all IBM PC-compatible personal computers, with most UEFI firmware
implementations providing support for legacy BIOS services. UEFI can support remote diagnostics and repair of
computers, even with no operating system installed. (source: Wikipedia)

## UEFI Drivers
Como qualquer outro SO, o UEFI tem drivers e eles são carregados pelo Clover ou OpenCore. Eles também devem carregar
dispositivos ou realizar outras tarefas, como carregar drives HFS da Apple com HfsPlus.efi, patching macOS's
boot.efi e assim por diante. Você pode encontrá-los como Clover Drivers ou
Drivers OpenCore, são todos drivers UEFI. (Nota: use apenas drivers que são feitos para isso
gerenciador de inicialização específico. Mais informações podem ser encontradas na página de conversão do trevo.

## EFI
It can denote two things: - Mac's firmware, which is the same as UEFI, but pretty modified for Macs
only, so not so "Universal"- The partition on your hard drive that stores software read by the UEFI to
load OSes (like the Windows bootloader) or UEFI Applications (like OpenCore), it's FAT32 formatted and has an
ID type of EF00 (in hex). It can be named ESP or SYSTEM, and it's usually from 100MB to 400MB in
size but the size doesn't reflect upon anything.

## MBR
O Master Boot Record é um tipo especial de setor de inicialização no início da massa do computador particionado
dispositivos de armazenamento como discos fixos ou unidades removíveis destinados ao uso com sistemas compatíveis com IBM PC e
além. O MBR foi introduzido pela primeira vez em 1983 com o PC DOS 2.0. O MBR contém as informações sobre como a lógica
partições, contendo sistemas de arquivos, são organizadas nesse meio. O MBR também contém código executável para
funcionar como um carregador para o sistema operacional instalado - geralmente passando o controle para o segundo carregador
estágio ou em conjunto com o registro de inicialização do volume de cada partição (VBR). Este código MBR é geralmente referido
como um gerenciador de inicialização (fonte: Wikipedia). Este formato é usado em configurações de BIOS / Legacy. O formato MBR suporta um
máximo de 2 TiB de tamanho e no máximo 4 partições primárias.

## GPT
Tabela de partição GUID (GPT) é um padrão para o layout de tabelas de partição de um armazenamento de computador físico
dispositivo, como uma unidade de disco rígido ou unidade de estado sólido, usando identificadores universalmente exclusivos, que também são
conhecidos como identificadores globalmente exclusivos (GUIDs). Fazendo parte da Interface de Firmware Extensível Unificada
(UEFI) padrão (substituição proposta do Fórum EFI Unificado para o BIOS do PC), no entanto, também é usado para
alguns sistemas BIOS, devido às limitações das tabelas de partição de registro mestre de inicialização (MBR), que usam 32 bits
para endereçamento de bloco lógico (LBA) de setores de disco tradicionais de 512 bytes (fonte: Wikipedia). Normalmente, este é
o formato de disco que você deseja usar em um sistema UEFI.


## EC
Embedded Controller. Comunica-se entre a placa principal e periféricos incorporados, como teclas de atalho, portas ou
bateria.

## PLUG
Permite que o gerenciamento de energia XCPM e Apple XNU seja conectado, permitindo um melhor controle geral da CPU. Apenas
compatível com Haswell e mais recentes.

## AWAC
ACPI Wake Alarm Counter Clock, clock interno da placa. Quase o mesmo que o Real-Time Clock (RTC). O Mac OS
não pode se comunicar com Clocks AWAC, então eles devem ser corrigidos (famosos Patches).

## PMC
Power Management Controller, nas placas-mãe B360, B365, H310, H370, Z390, os OEMs se esqueceram de mapear esta região e
então precisa SSDT-PMC para evitar falhas de page-falt.

## PNLF
Tela com luz de fundo interna, o macOS usa este dispositivo PNLF para enviar e receber informações para controle de brilho

## XOSI/_OSI
_OSI é usado para determinar qual sistema operacional está sendo inicializado, renomear para XOSI nos permite enganar o hardware
pensar que estamos inicializando um sistema operacional diferente

## HPET
High Precision Event Timer, Os sistemas operacionais usam isso para determinar como se comunicar com dispositivos (IRQ). macOS pode ser
muito exigente em como os dispositivos são configurados, por isso às vezes precisamos corrigir o HPET.

## RHUB
Root USB Hub, onde as portas USB são definidas. Se certas definições estiverem faltando aqui, as portas USB podem não funcionar
no macOS

## MEI
Intel Management Engine Interface,lida com tarefas diversas. No macOS, a Apple depende do IMEI para GPU Intel
aceleração. Se estiver usando um ID desconhecido, como um chipset da série 7 com Sandy Bridge, o macOS não conseguirá
encontre-o para aceleração de GPU.

## UNC
Uncore Bridge, semelhante a uma ponte norte, ele lida com muitas funções relacionadas ao cache. Muitas vezes, os OEMs terão
Com este dispositivo definido, mas não funcional, o macOS não é capaz de lidar com essas situações.

## SMBS
System Management Bus, usado para permitir que os dispositivos se comuniquem facilmente entre si.
