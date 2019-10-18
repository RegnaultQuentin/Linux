## Questions

- Connectez vous au host "proxy" avec vagrant et vérifier Comment est configuré le resolver dns du système ?

```
vagrant@proxy:/etc$ cat resolv.conf
nameserver 192.168.33.21
nameserver 192.168.33.22
```

- Retrouvez l'adresse ip du host `wiki.lab.local` avec la commande dig.
```
vagrant@proxy:/etc$ dig wiki.lab.local +short
192.168.56.11
```
- Connectez vous au host auth-1, quels sont les services réseaux qui sont en fonctionnement actuellement quels sont leur socket d'écoute ?

```
[vagrant@auth-1 ~]$ ss -tulp
Netid  State      Recv-Q Send-Q Local Address:Port                 Peer Address:Port      
udp    UNCONN     0      0            *:1006                       *:*
udp    UNCONN     0      0            *:domain                     *:*
udp    UNCONN     0      0      127.0.0.1:323                        *:*                  
udp    UNCONN     0      0            *:bootpc                     *:*
udp    UNCONN     0      0            *:bootpc                     *:*
udp    UNCONN     0      0            *:sunrpc                     *:*
udp    UNCONN     0      0            *:10130                      *:*
udp    UNCONN     0      0           :::1006                      :::*
udp    UNCONN     0      0           :::15661                     :::*
udp    UNCONN     0      0           :::domain                    :::*
udp    UNCONN     0      0          ::1:323                       :::*
udp    UNCONN     0      0           :::sunrpc                    :::*
tcp    LISTEN     0      50     127.0.0.1:mysql                      *:*                  
tcp    LISTEN     0      128          *:sunrpc                     *:*
tcp    LISTEN     0      128    192.168.33.31:http                       *:*              
tcp    LISTEN     0      128          *:domain                     *:*
tcp    LISTEN     0      128          *:ssh                        *:*
tcp    LISTEN     0      100    127.0.0.1:smtp                       *:*                  
tcp    LISTEN     0      128         :::sunrpc                    :::*
tcp    LISTEN     0      128         :::domain                    :::*
tcp    LISTEN     0      128         :::ssh                       :::*
tcp    LISTEN     0      100        ::1:smtp                      :::*
```
Leurs socket d'écoute ce trouve dans Local Address:Port et sont les :Port.

- Connectez vous au host recursor-1,  quels sont les services réseaux qui sont en fonctionnement actuellement quels sont leur socket d'écoute ?

```
Netid  State      Recv-Q Send-Q Local Address:Port               Peer Address:Port        
udp    UNCONN     0      0              *:1018                       *:*                   users:(("rpcbind",pid=1357,fd=10))
udp    UNCONN     0      0      192.168.33.21:53                         *:*                   users:(("pdns_recursor",pid=5949,fd=5))
udp    UNCONN     0      0      127.0.0.1:53                         *:*                   users:(("pdns_recursor",pid=5949,fd=4))
udp    UNCONN     0      0      127.0.0.1:323                        *:*                   users:(("chronyd",pid=1455,fd=1))
udp    UNCONN     0      0              *:68                         *:*                   users:(("dhclient",pid=5960,fd=6))
udp    UNCONN     0      0              *:68                         *:*                   users:(("dhclient",pid=2736,fd=6))
udp    UNCONN     0      0              *:111                        *:*                   users:(("rpcbind",pid=1357,fd=5),("systemd",pid=1,fd=62))
udp    UNCONN     0      0             :::1018                      :::*                   users:(("rpcbind",pid=1357,fd=11))
udp    UNCONN     0      0            ::1:323                       :::*                   users:(("chronyd",pid=1455,fd=2))
udp    UNCONN     0      0             :::111                       :::*                   users:(("rpcbind",pid=1357,fd=7),("systemd",pid=1,fd=64))
tcp    LISTEN     0      128            *:111                        *:*                   users:(("rpcbind",pid=1357,fd=4),("systemd",pid=1,fd=61))
tcp    LISTEN     0      128    192.168.33.21:53                         *:*                   users:(("pdns_recursor",pid=5949,fd=7))
tcp    LISTEN     0      128    127.0.0.1:53                         *:*                   users:(("pdns_recursor",pid=5949,fd=6))
tcp    LISTEN     0      128            *:22                         *:*                   users:(("sshd",pid=2373,fd=3))
tcp    LISTEN     0      100    127.0.0.1:25                         *:*                   users:(("master",pid=2588,fd=13))
tcp    LISTEN     0      128           :::111                       :::*                   users:(("rpcbind",pid=1357,fd=6),("systemd",pid=1,fd=63))
tcp    LISTEN     0      128           :::22                        :::*                   users:(("sshd",pid=2373,fd=4))
tcp    LISTEN     0      100          ::1:25                        :::*                   users:(("master",pid=2588,fd=14))

```
Pareil que dans la question du dessus.

- Où sont configuré chacuns de ces composants ?

Ils sont configuré dans /etc/pdns-recursor/
Il y a 2 fichiers `recursor.conf.orig` et `recursor.conf`

- Qu'est ce qui est configuré sur les serveurs recursifs pour le domaine lab.local ? (Important pour les Actions qui suivent)



- Comment mettre en évidence le fait que le récurseurs ne répondent que sur l’interface du réseaux back (192.168.33.0/24) ?

- Comment est sécurisé l’accès à mysql ?