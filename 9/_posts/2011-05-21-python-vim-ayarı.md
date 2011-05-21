---
layout: post
title: .vimrc ile vim'i özelleştirmek
---

Vim'i Python geliştirmeleri için daha verimli kullanmak mümkündür.
Vim'i kurmak için şu komutu kullanıyoruz:
sudo apt-get install vim-gnome
Daha sonra kullanıcı ev dizinine .vimrc dosyayı aşağıdakileri içerecek şekilde oluşturuyoruz:

syntax enable
filetype indent on
set et
set sw=4
set smarttab
map <f2> :w\|!python %<cr>

.py uzantılı bir dosyayı çalıştırmak için <F2> tuşunu kullanıyoruz.
