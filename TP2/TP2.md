A. Choix de l'algorithme de chiffrement

🌞 Déterminer quel algorithme de chiffrement utiliser pour vos clés

D'aprés ce site 
https://www.ethersys.fr/actualites/20241022-quelle-cle-ssh-generer/

le mielleur type de clé est l'ed25519


🌞 Générer une paire de clés pour ce TP

```
ssh-keygen -t ed25519 -f ~/.ssh/cloud_tp2
```

🌞 Configurer un agent SSH sur votre poste
```
eval 'ssh-agent'
ssh-add ~/.ssh/cloud_tp2
```

🌞 Connectez-vous en SSH à la VM pour preuve
```
maybelater@debian:~/Documents/efrei/B2/parc_informatique_cloud/TP2$ ssh -i ~/.ssh/cloud_tp2  azureuser@9.205.16.115
The authenticity of host '9.205.16.115 (9.205.16.115)' can't be established.
ED25519 key fingerprint is SHA256:5l0ygYGu2Nf3lS5RIQ7xiPVTBbULVwVX+Oy4DMV2UCg.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '9.205.16.115' (ED25519) to the list of known hosts.
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.17.0-1008-azure x86_64)
```


🌞 Créez une VM depuis le Azure CLI
``` 
az vm create -g TP2 -n vm2.2JA --size Standard_B1s --image almalinux:almalinux-x86_64:10-gen2:10.1.202512150 --admin-username maybelater --ssh-key-values tmp/ssh/cloud_tp2
```

🌞 Assurez-vous que vous pouvez vous connecter à la VM en SSH sur son IP publique
```
maybelater@debian:~/Documents/efrei/B2/parc_informatique_cloud/TP2$ ssh -i ~/.ssh/cloud_tp2 maybelater@9.205.153.239
The authenticity of host '9.205.153.239 (9.205.153.239)' can't be established.
ED25519 key fingerprint is SHA256:+poya3t23aPNTcmkUgi0XofH7cjjWXxAloxJx0lSy3g.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '9.205.153.239' (ED25519) to the list of known hosts.
[maybelater@vm2 ~]$ 
```

🌞 Une fois connecté, prouvez la présence...

```
[maybelater@vm2 ~]$ systemctl status waagent.service
● waagent.service - Azure Linux Agent
     Loaded: loaded (/usr/lib/systemd/system/waagent.service; enabled; preset: enabled)
     Active: active (running) since Mon 2026-03-23 10:07:25 UTC; 5min ago
● cloud-init.service - Cloud-init: Network Stage
     Loaded: loaded (/usr/lib/systemd/system/cloud-init.service; enabled; preset: enabled)
     Active: active (exited) since Mon 2026-03-23 10:07:25 UTC; 6min ago
```

🌞 Utilisez Terraform pour créer une VM dans Azure
```
maybelater@debian:~/Documents/efrei/B2/parc_informatique_cloud/TP2/terraform$ terraform plan

...

Plan: 8 to add, 0 to change, 0 to destroy.

────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run
"terraform apply" now.
maybelater@debian:~/Documents/efrei/B2/parc_informatique_cloud/TP2/terraform$ terraform apply 

...
Apply complete! Resources: 8 added, 0 changed, 0 destroyed.
```

```
maybelater@debian:~/Documents/efrei/B2/parc_informatique_cloud/TP2/terraform$ ssh -i ~/.ssh/cloud_tp2 maybelater@9.205.153.248
The authenticity of host '9.205.153.248 (9.205.153.248)' can't be established.
ED25519 key fingerprint is SHA256:zuF1zvkpBQRSuxUp6I48goKxiIeENy3k2f3ZundMOgA.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '9.205.153.248' (ED25519) to the list of known hosts.
[maybelater@vm3 ~]$ 
```