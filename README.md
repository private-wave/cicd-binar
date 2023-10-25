### HELLO WORLD

### Cara Setup Server

Bebas sesaui kebutuhan, tapi saya sarankan memakai ubuntu versi LTS(Long term Support)

### CARA BIKIN SSH

Generate an SSH Key Pair di Mac / Linux:

jalankan perintah dibawah ini untuk menggenerate sebuah key baru supaya kita bisa mengakses server dengan device kita

```bash
ssh-keygen -t rsa -b 2048
```

*NOTE: rsa => boleh di ganti dengan nama sebebas mungkin(untuk membedakan file ssh beberapa server), contoh biznet-gio, google-cloud, aws, dll

Setalah menjalankan perintah di atas, maka kalian bisa masuk ke folder ./.ssh dan lihat ada file bernama id_rsa => nama tergantung apa yang kalian bikin
```bash
nando@Barnandos-MacBook-Pro: /Users/nando/.ssh
➜   ls

config                     google_compute_engine.pub
digital_ocean_rsa          google_compute_known_hosts
digital_ocean_rsa.pub      id_rsa
gitlab_mashroom_key        id_rsa.pub
gitlab_mashroom_key.pub    known_hosts
google_compute_engine      known_hosts.old
```

setelah itu kita paste isi dari file ```id_rsa.pub``` di dalam server yang telah kalian bikin, di file ```~/.ssh/authorized_keys```

contoh isi dari ```~/.ssh/authorized_keys``` yang ada di server:
```bash
# Added by Google
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDtG8V7l5+bmqUkUuNUIfkW6BYYvMaRFKnPGN0Zxri8El+O4BouMXOLkYFMivaFfTMRPivI/1O7NqiWnygmd3skAgz+4qW4Yn8ngANMJPRF74+5J9s2pQsi71btsd/oqqwWXk1sJBLcrcBapq3NizUaPUelfFHVi4q26UuHu1t+Yz57uLZJIKrMsQbTKa2h9ooFAnQv7I7pjFENr1rTc9/SpwZ4P2hwH3WpIpe8E6sou8H6YE/o9405NxBv5ATmHHeHwk97bK1tGS3wUd6N............................nando@Barnandos-MacBook-Pro.local # nando adalah nama user, tergantung dari login mac/linux kalian
```

jika file ```~/.ssh/authorized_keys``` tidak, maka kalian bisa bikin file baru dengan folder sesuai user kalian

```bash
mkdir -p /home/nando/.ssh && touch /home/nando/.ssh/authorized_keys
```

Cara untuk konek kedalam server kalian
```bash
ssh -i ~/.ssh/id_rsa nando@34.101.253.102 # ssh -i ~/.ssh/id_<nama_ssh> <username>@<host>
```

Atau dengan cara langsung tanpa spesifik nama_ssh, jika kalian sudah mensetujui figerprint

Contoh fingerprint:
```bash
ssh -i ~/.ssh/id_rsa nando@34.101.253.102

The authenticity of host '34.101.253.102 (34.101.253.102)' can't be established.
ED25519 key fingerprint is SHA256:01A8JWEb4SJxKiDwlNpyk8lbb6il8qaGZ1t0z7CWSpA.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '34.101.253.102' (ED25519) to the list of known hosts.
```

```bash
ssh nando@34.101.253.102
```
### Cara Menyambungkan dengan github dengan server

Kalian bisa pergi ke repo > setting > scroll kebawah sampai ke secret > action

<img src="./.github/images/ss_1.png">

Setelah itu buat `New repository secret`

1. Buat lah secret `HOST` => atau di project ini bernama `SSH_HOST`, yang berisi ip address ```34.101.253.102```
1. Buat lah secret `PRIVATE_KEY` => atau di project ini bernama `SSH_PRIVATE_KEY`, yang berisi konten dar file `id_rsa` di dalam file `~/.ssh/id_rsa`
1. Buat lah secret `USER` => atau di project ini bernama `SSH_USER`, yang berisi username sesaui dengan user saat kalian bikin ssh ```nando```