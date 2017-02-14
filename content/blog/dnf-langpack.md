+++
date = "2016-08-09T18:43:27-03:00"
image = ""
math = false
title = "Instalando pacote de idiomas pelo dnf no Fedora 24"
tags = ["fedora", "i18n"]

+++
Para exibir as línguas já instaladas, execute no terminal:

`$ dnf langlist`

Para checar os pacotes de idiomas disponíveis:

`$ dnf langavailable`

Para informações das línguas instaladas:

`$ dnf langinfo [código da língua]`

ex:

`$ dnf langinfo pt_BR`

Para remover um língua:

`# dnf langremove [código da língua]`

E finalmente, para instalar o pacote de idiomas disponível para suas aplicações instaladas com o dnf, basta executar o seguinte comando no terminal:

`# dnf langinstall pt_BR`


feito.
