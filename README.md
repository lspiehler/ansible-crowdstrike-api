# Install Ansible
The example below is for RHEL/CentOS 8

```
sudo dnf -y install python3-pip
sudo pip3 install --upgrade pip
pip3 install ansible --user
```

# Clone Repo
```
git clone https://github.com/lspiehler/ansible-crowdstrike-api.git
cd ansible-crowdstrike-api
```
# Authenticate and get a JWT
### Set environment variables
```
export CSCLIENTID=yourapiclientid
export CSCLIENTSECRET=yourapisecret
```
### Example vars.yml file:
```
cat << EOF > vars.yml
CSAPIURL: https://api.crowdstrike.com
EOF
```
### Run the playbook
```
ansible-playbook auth.yml -e @vars.yml
```
Use the response from the previous command to set your JWT environment variable to be used for API requests
```
export CSACCESSTOKEN=iOjE2MTU5ODYzNzMsImlhdCI6MTYxNTg5OmJmIjoxNjE1ODk5OTczLCJpZGVZGVudGl0eSI6ImFkbWluIiwicmFuZCI6IjQwNDwNDNiMzBhLWNlZDItNGQyMi05YjczLTBRu1VFGbB3AlN7KVjb5DuK5qbfT_h0qBDgHceyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9hdCI6MTYxNTg5OTk3MywibmJmIjoxNjE1ODk5OTczLCJ
```
# List Assets
Modify the filter at the end of the URL in the get-devices.yml playbook and run it to get a list of devices matching the filter criteria
```
ansible-playbook get_devices.yml -e @vars.yml
```
# Run script on an endpoint
Modify the command string with your script contents and run the playbook
```
ansible-playbook run_script.yml -e @vars.yml
```