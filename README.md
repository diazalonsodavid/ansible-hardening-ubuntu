hardening_ubuntu
================

General hardening of all ubuntu systems.


Role Variables
--------------

Give a value for the variables:

These variables are found in:

bootloader_user:
bootloader_passwd:

These variables are the ones that will be requested at the start of the booter, at Grub boot.



In default/main.yml some variables are set for the initial cleaning of the packages and the installation of the apparmor packages.


***Encryption***

We can encrypt the variables inside the vars/main.yml file:

```console
ansible-vault encrypt_string 'variable_password' --name 'bootloader_passwd'
```

The above command will prompt you to enter a password for ansible-vault, which you will have to enter every time you run a playbook containing vault-encrypted passwords.

The command above creates this content:

```console
bootloader_passwd: !vault |
      $ANSIBLE_VAULT;1.1;AES256
      62313365396662343061393464336163383764373764613633653634306231386433626436623361
      6134333665353966363534333632666535333761666131620a663537646436643839616531643561
      63396265333966386166373632626539326166353965363262633030333630313338646335303630
      3438626666666137650a353638643435666633633964366338633066623234616432373231333331
      6564
```

That content is what you have to put in the variable file.

Every time you run a playbook you must add the --ask-vault-pass option and you will have to enter the ansible-vault password.

```console
ansible-playbook --ask-vault-pass playbook.yml -i inventories/hosts
```

If you prefer the option to encrypt an entire file you should run

```console
ansible-vault encrypt /vars/main.yml
```

You will be prompted to enter a password for ansible-vault which you will have to enter later to run the playbook.

```console
ansible-playbook --ask-vault-pass playbook.yml -i inventories/hosts
```


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: hardening_ubuntu, become: yes}

License
-------

license (MIT)


