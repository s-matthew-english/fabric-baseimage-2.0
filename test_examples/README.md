# Tricky Commands: Ansible

Running ansible playbook in localhost

Once we install ansible, we can start playing with it right away in the localhost. 
In production, we run stuffs against remote servers but knowing to play with localhost makes it easy and handy when we are learning ansible.

## Writing a hello world task

Lets first do it with ansible adhoc command and then convert the same into a playbook.

  ansible all -i "localhost," -c local -m shell -a 'echo hello world'
  
> localhost | success | rc=0 >>
> hello world

We’re using shell module to run ‘echo hello world’ in localhost. Now lets write a playbook helloworld.yml

---
- hosts: all
  tasks:
    - shell: echo "hello world"
    
## Running the playbook

  ansible-playbook -i "localhost," -c local helloworld.yml
  
> PLAY [all] *********

> GATHERING FACTS *********
> ok: [localhost]

> TASK: [shell echo "hello world"] *********
> changed: [localhost]

> PLAY RECAP *********
> localhost                  : ok=2    changed=1    unreachable=0    failed=0   

## Much simpler way to run

Wouldn’t it be cool if we just have to say ansible-playbook helloworld.yml instead of ansible-playbook -i "localhost," -c local helloworld.yml
It’s easy to do it using default inventory file /etc/ansible/hosts. Just add an entry for localhost as given below:
localhost ansible_connection=local
That’s it. Now run playbooks in localhost just by saying 
$ ansible-playbook helloworld.yml
and for adhoc command, 
$ ansible all -m shell -a 'echo hello world’
