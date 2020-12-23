SSH
=================================================================================

.. contents:: **Daftar Isi**

Install SSH 
---------------------------------------------------------------------------------

**Ubuntu**

::

	$ sudo apt-get install openssh-server

**Referensi**

- `Install ssh server di ubuntu`_


SSH Login Tanpa Password
---------------------------------------------------------------------------------

**SSH Key Pair**

Misalnya ada 2 buah komputer, client dan server. Komputer client ingin login ke
server menggunakan ssh tetapi tidak menggunakan password melainkan menggunakan
*public key*. Caranya adalah:

Pada komputer client:

- Generate SSH key pair

::

        ssh-keygen -t rsa -b 4096 -C "your_email@domain.com"

Secara *default* nama ssh file yang digunakan adalah id_rsa. Namun apabila
terdapat banyak ``id_rsa`` yang telah dibuat sebelumnya, maka simpanlah dengan nama
berbeda, misalnya ``id_rsa_baru``. Hasilnya *command* di atas akan menghasilkan
2 buah file yang bernama ``id_rsa_baru`` dan ``id_rsa_baru.pub``. File tanpa
*extension* adalah *private key* dan file dengan *extension* ``.pub`` adalah
*public key*.

- Buatlah config file 

::

        #baru
        Host namahost
                HostName namahost
                User namauser
                IdentityFile ~/.ssh/id_rsa_baru

Pastikan untuk mengisi ``HostName`` dan ``User`` secara benar. 

Pada komputer *server*:

- Copy *public key* dan *rename* menjadi ``authorized_keys``. Simpan file
  tersebut di ``~/.ssh/authorized_keys``. 

- Ganti *file permission**:

::

        $ chmod 700 ~/.ssh
        $ chmod 600 ~/.ssh/authorized_keys

**Tes Koneksi**

::

        $ ssh username@hostname

atau

::

        $ ssh username@ipaddress


**Referensi**

- `SSH Webpage <https://www.ssh.com/ssh/>`_
- `Use ssh login without key or password <https://www.techjunkie.com/ssh-login-without-key-password/>`_



.. Referensi


.. _`Install ssh server di ubuntu`: https://www.cyberciti.biz/faq/ubuntu-linux-install-openssh-server/
