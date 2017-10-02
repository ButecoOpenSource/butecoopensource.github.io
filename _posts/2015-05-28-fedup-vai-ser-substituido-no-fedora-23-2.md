---
layout: wordpress
title: Fedup vai ser substituído no Fedora 23
excerpt: |
  Artigo sobre nova abordagem da Red Hat sobre o atualizador Fedup, utilizado no Fedora
date: 2015-05-28 23:56:19
author: marcossouza
permalink: /fedup-vai-ser-substituido-no-fedora-23-2/
image: /assets/wp-content/uploads/2015/05/infinity-logo_400x400.png
categories:
  - Notícias
tags:
  - fedora
  - linux
  - release
---

Fedup é a ferramenta utilizada pelo Fedora para suas atualizações de sistema, e existe desde o Fedora 17. Entretanto, com a liberação do Fedora 23 sendo no fim deste ano, a ferramenta vai ser substituída nas novas releases do Fedora.

Embora o Fedup tenha melhorado muito desde a sua criação, os desenvolvedores do Fedora disseram que "o atual design é insustentável", e então estão planejando uma nova abordagem da ferramenta. O novo Fedup provavelmente vai baixar todos os pacotes da nova versão do Fedora e vai utilizar o recurso de "Atualizações Offline" do systemd para instalar estes novos pacotes. Este será feito provavelmente em conjunto com o PackageKit para ter uma melhor experiência do usuário.

Will Woods da Red Hat já tem um novo protótipo do novo atualizador do Fedora utilizando a nova abordagem como um plugin do DNF. Mais detalhes da mudanças planejadas do Fedup para o Fedora 23 pode ser encontrado na <a href="https://lists.fedoraproject.org/pipermail/devel/2015-May/210905.html" target="_blank">lista de desenvolvimento do Fedora</a>.

Via <a href="http://www.phoronix.com/scan.php?page=news_item&px=Fedora-Fedup-Being-Replaced" target="_blank">Phoronix</a>

Referências:
<a href="https://fedoraproject.org/wiki/FedUp" target="_blank">Fedup</a>
<a href="http://www.freedesktop.org/software/PackageKit/pk-intro.html" target="_blank">PackageKit</a>
<a href="http://www.freedesktop.org/wiki/Software/systemd/SystemUpdates/" target="_blank">Atualizações Offline - systemd</a>
<a href="https://fedoraproject.org/wiki/Features/DNF" target="_blank">DNF</a>