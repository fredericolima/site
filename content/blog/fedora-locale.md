+++
date = "2016-09-07T04:39:23-03:00"
image = ""
math = false
tags = ["fedora","locale","i18n"]
title = "Mudar o locale e o leiaute do teclado no Fedora 24"

+++

Exite um comando do systemd que facilita tudo na hora de definir o locale do sistema, ele é o localectl.

Exibe o locale e leiaute de teclado atual:

`$ localectl status`

Exibe os locales disponiveis instalados no sistema:

`$ localectl list-locales`

Define o locale para pt-BR

`# localectl set-locale LANG=pt_BR.utf8`

Exibe os leiautes de teclado disponíveis

`$ localectl list-keymaps`

Define o teclado para o padrão brasileiro no console e no X11

`# localectl set-keymap br`


