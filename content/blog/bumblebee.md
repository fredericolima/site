+++
Description = ""
FeaturedImage = ""
tags = ["fedora", "bumblebee"]
date = "2016-07-09T18:44:07-03:00"
title = "Instalando o Bumblebee no Fedora 24 com suporte ao Steam"
banner = "img/banners/bumblebee.png"

+++
Notebooks recentes com placas de vídeo da NVIDIA e processador i3, i5 ou i7 usam a tecnologia Optimus para aumentar a vida útil da bateria. Infelizmente o software que suporta essa tecnologia só foi desenvolvido para sistemas proprietários. 

O projeto Bumblebee é um conjunto de ferramentas desenvolvidas com o foco em fornecer suporte ao Optimus no Linux, até que os drivers do kernel suportem esse cenário. 

Este artigo ensina como instalar e utilizar o Bumblebee no Fedora 24 Workstation 64 bits e também com o Steam.

Para saber se você precisa do bumblebee, execute o comando abaixo:<br>
`$ lspci | grep -i vga`

Caso retorne mais de uma linha, sendo uma delas contendo a palavra NVIDIA, certamente você se enquadra nos requisitos para utilizar o Bumblebee.<br> 
Existem duas formas de se utilizar o Bumblebee, uma com os drivers livres nouveau, e a outra juntamente com os drivers proprietários da NVIDIA.<br>
Neste artigo, vamos cobrir a segunda opção. 

Primeiramente vamos adicionar o repositório do Bumblebee através do seguinte comando:<br> 
`# dnf -y --nogpgcheck install http://install.linux.ncsu.edu/pub/yum/itecs/public/bumblebee/fedora24/noarch/bumblebee-release-1.2-1.noarch.rpm`

Após isso, vamos instalar o pacote contendo o repositório do Bumblebee que contém os drivers proprietários da NVIDIA:<br> 
`# dnf -y --nogpgcheck install http://install.linux.ncsu.edu/pub/yum/itecs/public/bumblebee-nonfree/fedora24/noarch/bumblebee-nonfree-release-1.2-1.noarch.rpm`

Depois iremos instalar os pacotes multilib (entre outras coisas) do bumblebee e os drivers priprietários da nvidia. A versão multilib é ideal caso você queira executar pela placa de vídeo secundária, softwares/games 32 bits. 

Segue o comando:<br>
`# dnf install bumblebee-nvidia bbswitch-dkms VirtualGL.x86_64 VirtualGL.i686 primus.x86_64 primus.i686 kernel-devel`

Após a instalação, segue a sintaxe para utilizar a placa da NVIDIA:

utilizaremos o pacote primusrun (por ter uma performance melhor que o optirun). 
O "vblan_mode=0" irá aumentar o desempenho desabilitando a sincronização vertical. 
Ex:<br>
`# vblank_mode=0 primusrun xpto`

Aonde Xpto é o nome do jogo ou aplicativo no qual você quer que seja renderizado pela sua placa de vídeo da NVIDIA. 

Faça um teste para certificar que está tudo funcionando corretamente:<br>
`# vblank_mode=0 primusrun glxgears`

Steam: Caso você utilize o Steam como plataforma de games no Fedora 24, você não é aconselhado a executar o Steam via primusrun, mas sim apenas nos jogos. 
Como fazer isso? Executando o Steam normalmente, e dentro do Steam, ao selecionar o jogo, ir nas propriedades do jogo, e modificar o lançador do mesmo, para que cada vez que seja invocado o executável do jogo o primusrun também o seja. 

Para fazer o jogo utilizar a GPU da NVIDIA siga estes passos: 

1. Selecione o jogo – que você deseja executar utilizando a placa da NVIDIA – através da página Library do cliente Steam, clique com o botão direito, e selecione Properties.<br>
2. Clique no botão SET LAUNCH OPTIONS... e digite:<br>`vblank_mode=0 primusrun %command%`<br>
3. Salves as modificações.

Fontes: 

Acrelinux - Fedora - Instalando o Bumblebee [NVIDIA Optimus] - https://www.youtube.com/watch?v=sYn46YZmDrE<br> 
Fedora Project Wiki - https://fedoraproject.org/wiki/Bumblebee<br>
Steam - https://support.steampowered.com/kb_article.php?ref=6316-GJKC-7437&l=portuguese
