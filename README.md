1 Créer un répretoire Examen dans la home d'un utilisateur student
2 cloner le git dans celui-ci 
# Ansible
## Bootstrap
Il faut copier la pair de clefs dans le répertoire .ssh de votre utilisateur
Vous pouez faire eval $(ssh-agent) puis ssh-add de la clé privée. Le mot de passe est le même que l'utilisateur de la machine.
Ensuite vous devez copier la clef public sur les machines distantes -> ssh-copy-id -i /home/student/.ssh/exam_os.pub flairsou@10.1.72.124
Les identifiants et l'ip doivent chnager changer en fonction de la machine.
Pour faire le bootstrap de l'infra, se rendre dans bootstrap.
Une fois dans le répertoire,faire cette commande -> ansible-playbook -i hosts.yml bootstrap_playbook -K
le mot de passe qui est demandé est celui de l'utilisateur de la machine.

## Mails
Pour configurer les mails, se rendre dans msmtp.
une fois dans le répertoire, faire cette commande -> ansible-playbook -i hosts.yml playbook --ask-vault-pass
Le mot de passe du vault est : Tigrou007

## Docker avec rôle
Pour lancer l'installation de docker avec rôle, il faut se rendre dans le répertoire docker_role
Une fois dans ce répertoire, il faut faire cette commande -> ansible-playbook -i hosts.yml --tags arch docker_playbook
Attention que le "arch" va varier en fonction de la distribution, les possibilité sont arch ou debian ou fedora
L'installation ne se lance que sur la machine qui possède le tag.

# Docker
Pour réaliser Docker, se rendre dans le répertoire Docker.
Il vous faudra créer un répertoire "vol" qui va contenir le fichier index.html
une fois dans ce répertoire, faire cette commande -> docker build -t examen -f Dockerfile .
Puis cette commande -> docker run -v $(pwd)/vol:/app/root -p 0.0.0.0:8080:8080 -d examen
Pour tester il suffit de ce rendre sur cette page web -> http://"ip de votre machine":8080/