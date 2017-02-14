+++
date = "2016-07-15T21:57:34-03:00"
tags = ["fedora", "kernel","dnf"]
title = "Alterando a quantidade de kernels instalados simultaneamente no Fedora 24"
image = "img/banners/kernel-panic.png"
+++

As vezes ao iniciar o sistema, vemos o grub exibindo uma grande quantidade de entradas, com vários kernels. Realmente devemos deixar algum kernel antigo para caso uma versão nova tenha algum problema com nosso hardware (o que nunca aconteceu comigo). Mas apenas dois kernels já será o suficiente.

Nesse artigo vamos definir dois kernels para serem instalados no Fedora e não mais que dois.


Para listar todos os kernels instalados ordenados pela data de instalação ascendente digite:

`$ rpm -q --qf '%{installtime} %{installtime:date}: %{name}-%{version}%{release}\n' kernel | sort -n`


Para remover os kernels antigos de forma facilitada, instale o pacote yum-util:

`# dnf install yum-utils`


O comando package-cleanup remove os kernels antigos e o contador define quantas versões antigas vamos manter instalados:

`# package-cleanup --oldkernels --count=2`


Agora vamos definir quantos kernels vamos permitir ao DNF instalar por padrão, editando a diretiva installonly_limit do arquivo /etc/dnf/dnf.conf:

`installonly_limit=2`


Fontes:

http://superuser.com/questions/767008/fedora-get-a-list-of-installed-kernels-by-date

http://www.if-not-true-then-false.com/2012/delete-remove-old-kernels-on-fedora-centos-red-hat-rhel/
