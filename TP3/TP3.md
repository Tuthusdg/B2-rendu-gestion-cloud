🌞 Créez une VM azure (une commande az)
```
az vm create -g TP3 -n vm3.A --size Standard_B1s --image almalinux:almalinux-x86_64:10-gen2:10.1.202512150 --admin-username maybelater --ssh-key-values tmp/ssh/cloud_tp2
```
🌞 Connexion SSH
``` 
maybelater@debian:~/Documents/efrei/B2/parc_informatique_cloud/TP3$ ssh -i ~/.ssh/cloud_tp2 maybelater@9.205.153.169
The authenticity of host '9.205.153.169 (9.205.153.169)' can't be established.
ED25519 key fingerprint is SHA256:tgkBmYDBWbAy1pDov7ZMYxQlVjR+CDBMQypDkif2b5M.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '9.205.153.169' (ED25519) to the list of known hosts.

1 device has a firmware upgrade available.
Run `fwupdmgr get-upgrades` for more information.
```

les commandes suivantes doivent être dispos : htop, vim, dig, ping
```
[maybelater@vm3 ~]$ htop --v
htop 3.3.0
[maybelater@vm3 ~]$ dig --v
Invalid option: --v
Usage:  dig [@global-server] [domain] [q-type] [q-class] {q-opt}
            {global-d-opt} host [@local-server] {local-d-opt}
            [ host [@local-server] {local-d-opt} [...]]

Use "dig -h" (or "dig -h | more") for complete list of options
[maybelater@vm3 ~]$ vim --v
VIM - Vi IMproved 9.1 (2024 Jan 02, compiled Feb 25 2026 00:00:00)
Unknown option argument: "--v"
More info with: "vim -h"
[maybelater@vm3 ~]$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=52 time=10.0 ms
```

```
[maybelater@vm3 ~]$ sudo cloud-init clean --logs
```