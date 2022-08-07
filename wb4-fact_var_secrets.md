## Facts
- Create a playbook named "facts.yml"
ansible-playbook facts.yml -i inventory

- Create a playbook named ip.yml
ansible-playbook ip.yml -i inventory


## Secret

- Create encypted variables using "ansible-vault" command

# Get the hashed password for user password
python -c 'import crypt; print crypt.crypt("This is my Password", "$1$SomeSalt$")'

ansible-vault create secret.yml

# Enter data to store as encrypted
username: user1
password: $1$SomeSalt$I7blsh5Z6ce6AjTyZI9r41 #output from python

- Check the file
cat secret.yml
# Viewing
ansible-vault view  secret.yml

## Using Secrets 

create a file named "create-user.yml”

ansible-playbook create-user.yml -i inventory

# Error
ERROR! Attempting to decrypt but no vault secrets found

Run the playbook with "--ask-vault-pass" command:

ansible-playbook --ask-vault-pass create-user.yml -i inventory

# Verify the user created
`ansible all -b -m command -a "grep user1 /etc/shadow" -i inventory`

