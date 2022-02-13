---
title: "Libertando uma Fonera"
date: "2009-05-17"
categories: 
  - "free-sw"
tags: 
  - "fonera"
  - "free-sw"
  - "openwrt"
---

A minha velhinha [Fonera 2100A](http://images.google.pt/images?q=fonera%202100A) já mais que merecia ser libertada, mas só recentemente a libertei das amarras proprietárias da Fon. Procurei pelas instruções no [wiki do OpenWRT para a modelo 2100A](http://oldwiki.openwrt.org/OpenWrtDocs(2f)Hardware(2f)Fon(2f)Fonera.html), mas o "oldwiki" do OpenWRT peca precisamente naquele problema que os Wikis por vezes têm a tendência em falhar: comentários pelo meio do texto importante, algumas experiências documentadas de forma confusa, etc.

Daí que após algumas procuras mais, encontrei um [excelente site com uma explicação passo a passo](http://www.hermerschmidt.com/Linux/HowtoFlashFoneraWithOpenWrt), embora ainda assim necessitasse de alguns ajustes. Segue então o que eu fiz diferente, de acordo com a numeração da explicação:

**1: Recuperar o acesso ao sistema.**

- _senha do root_: estava com um problema... mudei recentemente a password e esqueci-me. Felizmente podia recuperar o firmware original pressionando no 'reset' durante cerca de 30s.
- _controlo do sistema_: a forma de recuperar a senha do root também recuperava o sistema original, a release **0.7.1 r1**, cujo interface web é vulnerável à injecção de comandos, permitindo iniciar o servidor de ssh. As [instruções aqui são para 0.7.2 r3, mas envolvem o downgrade para a 0.7.1 r1](http://www.fonerahacks.com/index.php/Tutorials-and-Guides/How-to-enable-SSH-on-version-0.7.2-r3.html), bastando começar a partir desse passo em vez de desde o início.

**2: remover o DRM substituíndo o bootloader**

No meu caso o 3º passo não funcionou, onde então foi necessário saltar o 4º passo, fazer o 5º e o 6º, por fim voltando ao 2º e 3º.

**3: instalar o OpenWRT** Para mim os tamanhos especificados para as partições não batiam certo, ficando com espaço a menos. Receando fazer uma asneira que tornasse a Fonera num "tijolo", procurei por mais gente com o mesmo problema e encontrei umas boas [sugestões de tamanhos](http://forum.openwrt.org/viewtopic.php?id=10942), que me permitiram completar a instalação com sucesso:

> RedBoot> **fis init** About to initialize \[format\] FLASH image system - continue (y/n)? **y** \*\*\* Initialize FLASH Image System ... Erase from 0xa87e0000-0xa87f0000: . ... Program from 0x80ff0000-0x81000000 at 0xa87e0000: . RedBoot> **load -r -v -b %{FREEMEMLO} openwrt-atheros-root.squashfs** Using default protocol (TFTP) - Raw file loaded 0x80040800-0x801e07ff, assumed entry at 0x80040800 RedBoot> **fis create -f 0xA8030000 -l 0x006F0000 rootfs** ... Erase from 0xa8030000-0xa8720000: ............................................................................................................... ... Program from 0x80040800-0x801e0800 at 0xa8030000: .......................... ... Erase from 0xa87e0000-0xa87f0000: . ... Program from 0x80ff0000-0x81000000 at 0xa87e0000: . RedBoot> **load -r -v -b %{FREEMEMLO} openwrt-atheros-vmlinux.lzma** Using default protocol (TFTP) - Raw file loaded 0x80040800-0x801007ff, assumed entry at 0x80040800 RedBoot> **fis create -r 0x80041000 -e 0x80041000 vmlinux.bin.l7** ... Erase from 0xa8720000-0xa87e0000: ............ ... Program from 0x80040800-0x80100800 at 0xa8720000: ............ ... Erase from 0xa87e0000-0xa87f0000: . ... Program from 0x80ff0000-0x81000000 at 0xa87e0000: . RedBoot> **fis load -l vmlinux.bin.l7** Image loaded from 0x80041000-0x80282085 RedBoot> **exec**

Lançado o exec, que ainda demorou cerca de 20 minutos, tinha uma Fonera com OpenWRT pronta para o que necessitasse.

Neste momento tenho-a preparada para 2 cenários:

1. partilha do meu acesso à Internet (melhor que a rede Fonera por ser aberta), mas não a tempo inteiro :)
2. partilha de um link de rede para algum evento.
