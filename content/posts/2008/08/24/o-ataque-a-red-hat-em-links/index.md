---
title: "O ataque à Red Hat/Fedora em Links"
date: "2008-08-24"
categories: 
  - "free-sw"
tags: 
  - "free-sw"
  - "security"
---

1. Os sistemas deixam de estar disponíveis. Um posterior (alguns consideram tardio) [aviso na Fedora Announce](https://www.redhat.com/archives/fedora-announce-list/2008-August/msg00008.html) denúncia um problema de segurança com pacotes «_as a precaution, we recommend you not download or update any additional packages on your Fedora systems_»
2. Enquanto [a investigação prossegue](https://www.redhat.com/archives/fedora-announce-list/2008-August/msg00009.html) à porta fechada, possivelmente por motivos legais, [os sistemas vão lentamente voltando a funcionar](https://www.redhat.com/archives/fedora-announce-list/2008-August/msg00011.html)
3. Finalmente (8 dias depois do anúncio oficial) [revelam o que aconteceu](https://www.redhat.com/archives/fedora-announce-list/2008-August/msg00012.html): alguém conseguiu penetrar no sistema de compilação automática de software.
4. Conseguiram submeter pacotes de OpenSSH assinados com a chave da Red Hat, mas em princípio não chegaram a ser distribuídos. Publicaram [novos pacotes de OpenSSH](http://rhn.redhat.com/errata/RHSA-2008-0855.html) e um [script para verificar](http://www.redhat.com/security/data/openssh-blacklist.html) se por azar algum um cliente de Red Hat Enterprise Linux chegou a descarregar esses pacotes.

É mau? Sim, é mau. Mas o pior que aconteceu foi um beliscão na imagem da Red Hat. Já passo.

Sem dúvida seguir-se-ão as piadas do costume na Internet (Debian passou por isso recentemente, embora no seu caso tivesse sido bem mais grave), até que a moda canse ou seja substituída por outro evento.

Felizmente foi detectado atempadamente e, mais importante ainda, não conseguiram acesso às [chaves da Red Hat. Estão preservadas num HSM](http://www.awe.com/mark/blog/200701300906.html) (High Security Module), apenas conseguiram submeter pacotes corrompidos para o sistema de assinatura automática.

_Move along..._
