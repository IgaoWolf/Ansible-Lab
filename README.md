# Ansible Laboratório

Neste laboratório, você utilizará uma máquina virtual como servidor Ansible para gerenciar e automatizar suas configurações.

## 1. Atualizar o Sistema

Primeiro, atualize os pacotes do sistema:

```bash
sudo apt update
sudo apt upgrade
```
## 2. Instalar o Ansible

Instale o Ansible:

```bash

sudo apt install ansible
```

Verifique a versão do Ansible instalada:

```bash

ansible --version
```

A saída esperada deve ser semelhante a:

```bash

ansible [core 2.16.3]
  config file = None
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.12.3 (main, Apr 10 2024, 05:33:47) [GCC 13.2.0] (/usr/bin/python3)
  jinja version = 3.1.2
  libyaml = True
```

## 3. Criar Usuário para Gerenciamento

Crie um usuário que será utilizado para gerenciar os servidores:

```bash

sudo adduser ansible-user
```

Conceda privilégios administrativos ao usuário:

```bash

sudo usermod -aG sudo ansible-user
```

Verifique se o usuário foi criado corretamente:

```bash

getent passwd ansible-user
```

Senha do usuário: teste-ansible
## 4. Instalar sshpass

Instale o sshpass, que pode ser necessário para automatizar a autenticação SSH:

```bash

apt-get update
apt-get install sshpass
```

## 5. Verificar Inventário

Use o comando ansible-inventory para garantir que o inventário foi configurado corretamente:

```bash

ansible-inventory --list
```

## 6. Testar Conectividade

Teste a conectividade com todos os hosts no inventário:

```bash

ansible all -m ping
```

## 7. Executar Playbooks

Execute os seguintes playbooks conforme necessário:

    Instalar aplicativos no cliente 1:

```bash

ansible-playbook install_apps_cliente1.yml --extra-vars "ansible_sudo_pass=teste-ansible"
```

Obter informações de CPU para o grupo clientes:

```bash

ansible-playbook cpu_info_clientes.yml
```

Obter informações de discos para o grupo clientes:

```bash

ansible-playbook discos_info_clientes.yml
```

Obter informações de df -h de um host específico (IP ou nome):

```bash

ansible-playbook df_h_prompt.yml --extra-vars "target_host=192.168.3.102"
```

Instalar e configurar o chronyd no grupo clientes:

```bash

ansible-playbook install_configure_chronyd.yml --extra-vars "ansible_sudo_pass=teste-ansible"
```

Definir o timezone no servidor para America/Sao_Paulo:

```bash

ansible-playbook set_timezone.yml --extra-vars "ansible_sudo_pass=teste-ansible"
```

Instalar e configurar um agente Zabbix:

```bash

ansible-playbook install_config_zabbix.yml --extra-vars "ansible_sudo_pass=teste-ansible"
```

