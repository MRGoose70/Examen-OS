1 Créer un répretoire Examen dans la home d'un utilisateur student
2 cloner le git dans celui-ci 
# Ansible
## Bootstrap
Il faut copier la pair de clefs dans le répertoire .ssh de votre utilisateur
Vous pouez faire eval $(ssh-agent) puis ssh-add de la clé privée. Le mot de passe est le même quue l'utilisateur de la machine.
Pour faire le bootstrap de l'infra, se rendre dans bootstrap.
Une fois dans le répertoire,faire cette commande -> ansible-playbook -i hosts.yml bootstrap_playbook -K
le mot de passe qui est demandé est celui de l'utilisateur de la machine.

## Mails
Pour configurer les mails, se rendre dans msmtp.
une fois dans le répertoire, faire cette commande -> ansible-playbook -i hosts.yml playbook --ask-vault-pass

# Docker
Pour réaliser Docker, se rendre dans le répertoire Docker.
Il vous faudra créer un répertoire "vol" qui va contenir le fichier index.html
une fois dans ce répertoire, faire cette commande -> docker build -t examen -f Dockerfile .
Puis cette commande -> docker run -v $(pwd)/vol:/app/root -p 0.0.0.0:8080:8080 -d examen
Pour tester il suffit de ce rendre sur cette page web -> http://<ip de votre machine>:8080/
