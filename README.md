# TestMongoDBLookup

Just a little test for the mongodb lookup plugin for PR: https://github.com/ansible/ansible/pull/46579

Get a test MongoBD instance running in docker with the following (no auth)...

```
docker run -tid --mount source=mongo,target=/var/lib/mongo --rm -p 27017:27017 --name mongodb rhyscampbell/dockermongodb
```


```
virtualenv venv
source venv/bin/activate
pip install ansible
ansible-playbook -l localhost test_mongodb.yml
```

Throws following error...

> fatal: [localhost]: FAILED! => {"msg": "An unhandled exception occurred while running the lookup plugin 'mongodb'. Error was a <class 'ansible.errors.AnsibleError'>, original message: pymongo is required in the master node (this machine) for mongodb lookup."}

```
pip install pymongo
```

Now playbook run should work...

```
ansible-playbook -l localhost test_mongodb.yml
```
