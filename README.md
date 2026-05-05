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
