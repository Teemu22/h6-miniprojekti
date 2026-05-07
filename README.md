# h6-miniprojekti - Linux setup automation with Ansible

## Kuvaus
Tässä projektissa toteutetaan Linux-ympäristön automatisoitu käyttöönotto Ansiblea hyödyntäen. Playbook asentaa keskeiset
ohjelmat ja käynnistää SSH-palvelun yhdellä komennolla.

## Mitä projekti tekee
- asentaa OpenSSH-serverin
- asentaa curl-paketin
- asentaa Gitin
- käynnistää SSH-palvelun

## Vaatimukset
- Linux-järjestelmä
- Ansible asennettuna
- Sudo-oikeudet

## Käyttö

1. Kloonaa projekti: git clone git@github.com:Teemu22/h6-miniprojekti.git
   cd h6-miniprojekti/ansible

2. Aja playbook: ansible-playbook site.yml -K

3. Syötä käyttäjän salasana pyydettäessä: (BECOME password:)

Playbook asentaa tarvittavat paketit ja käynnistää SSH-palvelun automaattisesti.

## Koodi ja niiden tarkoitus

- `site.yml` sisältö on verrattavissa navigaattoriin ja käytännössä se kertoo Ansiblelle mitä rooleja ajetaan ja mille koneille

site.yml koodi:

```bash
- hosts:all
  become: true
  roles:
    - common
```
- `main.yml` puolestaan sisältää kaikessa yksinkertaisuudessaan ohjeet, mitkä tekevät varsinaisen työn ja ohjaavat meidät perille asti

main.yml koodi:

```yaml
- name: Install packages
  apt:
    name:
      - openssh-server
      - curl
      - git
    state: present
    update_cache: true

- name: Start SSH service
  service:
    name: ssh
    state: started
    enabled: true
````

- Projektissa käytettiin myös `ansible.cfg`-tiedostoa. Se määrittää Ansiblen oletusasetuksia ja kertoo Ansiblelle mitä inventory-tiedostoa käytetään.

ansible.cfg:

```ini
[defaults]
inventory = hosts.ini
```

- `hosts.ini` on hyvin ihmismäisesti selitettynä lista koneita, joita ansible hallitsee

hosts.ini:

```ini
localhost ansible_connection=local

[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

````
h6-miniprojekti/
├── LICENSE
├── README.md
└── ansible/
    ├── ansible.cfg
    ├── hosts.ini
    ├── site.yml
    └── roles/
        └── common/
            └── tasks/
                └── main.yml
````

- Tämä kaikki on projektimme rakenne. Lopuksi pitää tietenkin ajaa ansible-playbook ja varmistaa idempotenssi, ajettuamme on hyvä aina todeta ettei mikään muuttunut ja tila on vakaa.

## Lähteet

Ansible Documentation – Introduction to Playbooks  
https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html

Ansible Documentation – apt module  
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_module.html

Ansible Documentation – service module  
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/service_module.html

Ansible Documentation – Inventory  
https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html

Ansible Documentation – Ansible Configuration Settings  
https://docs.ansible.com/ansible/latest/reference_appendices/config.html

Tero Karvinen – Hello Ansible  
https://terokarvinen.com/2023/hello-ansible/
