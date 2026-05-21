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


# References
