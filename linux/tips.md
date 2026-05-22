Previous: [Linux](linux.md)  

# Useful Annotation

##### Check versions

```
    $ lsb_release -a // versão do linux
    $ uname -m // arquitetura do processador
    $ uname -r // versão do kernel linux
    $ ldd --version // check glib version
```

##### Adicionando usuário na lista de sudoers

```
    user@Debian:~$ su -
```

Digite a senha do root.

```
    $root@debian:~# usermod -aG sudo takeshi
```

##### Alterando as permissões após copiar um diretório de ```/media``` para um diretório do sistema

Ao copiar um diretório de ```/media``` (dispositivos externos como USB) para um diretório do sistema, o sistema mantém as permissões e propriedaddes originais.

```
  $ cd /media/your_dir /home/$user
  $ sudo chown -R $user:$user /home/$user/your_dir
```


# References
