# Ansible-Laboratorio
 
Neste laborátorio, estou utilizando uma máquina virtual para servir de Servidor Ansible.

# Para instalação é muito simples, básicamente será necessário rodar os comandos abaixo:

sudo apt update
sudo apt upgrade

sudo apt install ansible

# ansible --version
ansible [core 2.16.3]
  config file = None
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.12.3 (main, Apr 10 2024, 05:33:47) [GCC 13.2.0] (/usr/bin/python3)
  jinja version = 3.1.2
  libyaml = True

# Em todos os servidores que serão gerenciados pelo Ansible, utilizará o seguinte usuário 
sudo adduser ansible-user

# Fornecendo privilegios administrativos para o usuário
sudo usermod -aG sudo ansible-user

# Checar se o usuário foi criado corretamente
getent passwd ansible-user

##senha 
teste-ansible

# Será necessário instalar o sshpass
apt-get update
apt-get install sshpass

# Use o comando ansible-inventory para garantir que o inventário foi configurado corretamente:
ansible-inventory --list

# Para testar a conectividade com todo o inventario rode o seguinte comando 
ansible all -m ping

# Para utilizar o install_apps_client1, irá utilizar o grupo que está no host's

ansible-playbook install_apps_cliente1.yml --extra-vars "ansible_sudo_pass=teste-ansible"

# Para puxar todos as informações dos CPU para o grupo clientes que está nos host's

ansible-playbook cpu_info_clientes.yml

# Para puxar todos as informações dos discos para o grupo clientes que está nos host's

ansible-playbook discos_info_clientes.yml

# Para puxar as informações de um df -h de um host em especifico (ip ou name)

ansible-playbook df_h_prompt.yml --extra-vars "target_host=192.168.3.102"
