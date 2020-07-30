---
layout: post
title: Conhecendo o Btrfs
date: 2020-07-31 08:00:00
categories: Desenvolvimento
tags:
  - Sistemas de Arquivos
  - FS
  - Ext
  - XFS
  - Btrfs
  - Linux
permalink: conhecendo-o-btrfs
author: marcossouza
header:
  overlay_color: "#666666"
  show_overlay_excerpt: false
  image: /assets/content/btrfs-logo.png
---

O sistema de arquivos Btrfs foi criando em 2007, por engenheiros que trabalhavam na Oracle e FusionIO. Ele foi concebido com a ideia de ter um sistema de arquivos que provesse funcionalidades semelhantes ao o que o ZFS já oferecia no Solaris e variantes do BSD.

Este artigo tem como foco mostrar algumas funcionalidades que tornam o Btrfs um sistema de arquivos tão interessante para usuários avançados de Linux, e está em vias de se tornar o próximo sistema de arquivos padrão em distribuições Linux. Para não deixar o artigo longo demais, referências serão adicionadas no final detalhando os assuntos aqui tratados. Enfim, vamos às funcionalidades.

## Copy-on-write

Sistemas de arquivo como o Ext4 e XFS utilizam o que se chama de "atualização in place", ou seja, gravam alterações de dados no local do disco em que o dado se encontrava antes de ter sido alterado.

Btrfs utiliza o recurso *Copy-on-Write* (cópia em gravação), desta forma ao gravar uma alteração em um arquivo, o Btrfs escolhe um local diferente do que o usado atualmente, e após a gravação ser concluída ele atualiza as referências do sistema de arquivos para este novo local.

A utilização desta estratégia visa evitar problemas de dados parcialmente escritos quando  acontecer um crash no sistema ou uma falta de energia. No pior dos casos, somente os dados que não foram atualizados para o novo local são perdidos, não corrompendo o sistema. Por padrão, o Btrfs escreve os dados em memória no disco a cada 30 segundos, ou se houver um grande número de alterações acumuladas em memória.

## Subvolumes

Imagine um subvolume como se fosse uma partição de disco, mas totalmente gerenciado pelo mesmo sistema de arquivos, contendo sistemas de arquivos independentes e podendo até mesmo utilizar quota para definir limites de uso.

Para o usuário do sistema, os subvolumes são como diretórios comuns, podendo inclusive conter subvolumes dentro de outro subvolumes.

Como um sistema de arquivos pode ter muitos subvolumes, existe uma opção para montar utilizando um subvolume específico. A fim de simplificar este uso, o Btrfs permite configurar um subvolume como padrão, para que quando o disco for montado sem especificar nenhum subvolume, o definido como padrão será utilizado.

Distribuições Linux como o openSUSE se utilizam deste recurso para criar um subvolume na raiz do sistema, ou `/`, e dentro deste criar outros subvolumes para diretórios importantes como `/var`, `/home`, `/root`, `/opt`, entre outros. O subvolume do `/` é colocado como padrão neste método de instalação.

## Snapshots

Um snapshot não passa de um subvolume com um conteúdo inicial, ao contrário de um subvolume comum que não tem nenhum conteúdo após sua criação. Um Snapshot é utilizado para criar uma imagem, um ponto no tempo de vida de um subvolume. Este é um recurso interessante para criação de pontos de restauração, ou seja, pode-se criar um snapshot antes de atualizar o sistema, e se algo não ocorrer como desejado pode-se voltar para uma versão anterior.

O openSUSE utiliza snapshots para gerenciar as atualizações de sistema. Cada vez que o Zypper (gerenciador de pacotes) é executado para atualizar pacotes, um snapshot é criado antes e depois da atualização, permitindo que o usuário reinicie o sistema a partir de um ponto antes da atualização, caso seja necessário.

Ao utilizar recursos de Copy-On-Write, snapshots não consomem muito espaço adicional de disco, somente incrementando o número de referências para o mesmo bloco de dados. Quando partes de um arquivo são alterados em um snapshot, este sendo diferentes do arquivo original do subvolume, novos blocos de dados serão alocados para este arquivo em particular.

Snapshots podem ser criados em modo leitura e leitura/escrita, podendo inclusive aninhar snapshots dentro de outros snapshots e misturando estes modos conforme necessário (criar um snapshot leitura a partir de um snapshot leitura/escrita).

## Compressão

O Btrfs suporta compressão dos dados de forma transparente para o usuário. Atualmente suporta os seguintes algoritmos de compressão: LZO, zlib e Zstd. No caso do zlib e Zstd ainda pode-se dizer o nível de compressão, sendo o zlib de 1 até 9, enquanto o Zstd tem valores de 1 até 15. Ao utilizar um valor mais alto implica em uma melhor taxa de compressão, mas também no aumento do uso de memória.


## Gerenciamento de discos

Outros sistemas de arquivo do Linux como Ext4, XFS ou fat trabalham em cima de um único disco. Se o usuário desejar utilizar recursos como RAID 10, este deve recorrer ao *md* (multi device) para criar um disco virtual contendo dois discos, e só então montar o seu sistema de arquivos sobre este disco virtual.

O Btrfs possui um gerenciador de discos embutido no sistema, permitindo o usuário adicionar e substituir discos com o sistema sendo utilizado e até trocar entre perfis de RAID.

Por padrão, Btrfs utiliza RAID 1 para metadados, mesmo que o sistema estiver utilizando somente um disco. Desta forma se por acaso uma cópia do metadata sendo acessado estiver corrompida, o Btrfs pode tentar a segunda cópia.

## Checksum

Um checksum (ou soma de verificação) é uma técnica utilizada para verificar integridade de dados. Por padrão, o Btrfs faz checksum de dados e metadados no momento da escrita no disco. Se o sistema de arquivos detectar um checksum inválido ao tentar ler um arquivo (se o dado estiver corrompido), ele automaticamente procura por outra cópia do mesmo dado em outro disco. Se encontrar, ele automaticamente corrige o local onde encontrou o problema, reescrevendo o dado na posição onde ele estava corrompido.

Vale ressaltar que o Btrfs armazena mais de uma cópia do arquivos somente se estiver utilizando uma configuração de RAID.

## Send e Receive

O rsync é uma ferramenta conhecida por sincronizar dados entre diferentes máquinas. Esta ferramenta checa diferenças entre versões de arquivos e se por acaso os mesmos tiverem quais diferenças uma nova cópia do arquivo é enviada.

A funcionalidade send to Btrfs cria um arquivo de operações a serem aplicadas em um sistema de arquivos, transmitindo somente o que foi alterado. Por exemplo, se um arquivo tipo ISO tiver o owner alterado, o rsync enviará o arquivo novamente pela rede. Se a ferramenta send for utilizada, ela criará um arquivo contendo somente um comando chown que será aplicado no lado remoto utilizando a ferramenta receive. Para mais informações sobre esta funcionalidade verifique a seção de referências.

## Superblock

Todo sistema de arquivos contém um superblock. Este é responsável por guardar informações do sistema de arquivos como um todo, como espaço utilizado, tamanho do bloco de dados utilizado, e outras informações específicas para cada sistema de arquivos. Se por acaso o superblock for danificado ou corrompido, existe uma grande chance dos seus dados terem sido perdidos.

A fim de evitar que isso aconteça, um sistema Btrfs guarda três cópias do superblock em locais diferentes do disco: 64k, 256Mb e 256Gb. Estes valores são relacionados a posição física do disco.

## Converter um sistema de arquivos para Btrfs

É possível converter sistemas Ext2/Ext3/Ext4 e reiserfs para Btrfs utilizando a ferramenta Btrfs-convert. A ferramenta opera diretamente no disco, salvando o conteúdo original de um subvolume com o nome `<sistema_de_arquivos>_saved`. Para mais informações sobre este recurso acesse [esta página](https://btrfs.wiki.kernel.org/index.php/Conversion_from_Ext3) da wiki do Btrfs.

## Conclusão

Como podemos ver, o Btrfs tem muitos recursos interessantes se o compararmos com outros sistemas de arquivo mais utilizados atualmente. Vale salientar ainda que existem muitos outros recursos que não foram mencionados neste artigo. Para os mais interessados, vale a pena dar uma olhada na [wiki do Btrfs](https://btrfs.wiki.kernel.org/index.php/Main_Page) e nas referências abaixo.

## Referencias

- [Copia em gravacao](https://pt.wikipedia.org/wiki/C%C3%B3pia_em_grava%C3%A7%C3%A3o)
- [Manual do comando para gerenciar subvolumes e snapshots](https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs-subvolume)
- [Manual do openSUSE sobre gerenciamento de snapshots](https://doc.opensuse.org/documentation/leap/archive/15.0/reference/html/book.opensuse.reference/cha.snapper.html)
- [Manual do Btrfs sobre como criar um sistema de arquivos com multiplos discos](https://btrfs.wiki.kernel.org/index.php/Using_Btrfs_with_Multiple_Devices)
- [Exemplo de uso de send/receive](https://mpdesouza.com/2020/05/14/btrfs-making-send-more-capable/)
- [Manual da ferramenta Btrfs-convert](https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs-convert)
- [Link descrevendo localização das cópias de superblock](https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs-convert)
- [Página da wiki do Btrfs sobre compressão e suas configurações](https://btrfs.wiki.kernel.org/index.php/Compression)
- [Checksum, ou soma de verificação](https://pt.wikipedia.org/wiki/Soma_de_verifica%C3%A7%C3%A3o)
