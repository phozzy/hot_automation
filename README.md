# hot_automation
automation of server provisioning in openstack cloud with ansible and jenkins.

ansible vault password: `12345`

`tuser.yml` content:
```
---
# your user credentials in your domain
ipa_user: tuser
ipa_pass: very_strong_password
# next parameters are from your openstack cloud
os_auth_url: "url given you by openstack provider"
os_username: "username given you by openstack provider"
os_password: "very strong password given you by openstack provider"
os_project_id: "id of your project in openstack cloud"
os_project_name: "your project name in openstack cloud"
os_user_domain_name: "user name in you domain in openstack cloud"
...
```
