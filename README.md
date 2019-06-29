# piphonom_infra
piphonom Infra repository

************

bastion_IP = 35.210.212.166
someinternalhost_IP = 10.132.0.3

************

To connect to someinternalhost in one command through the bastion host 
you can use command:

ssh -i ~/.ssh/otusdevops otusdevops@10.132.0.3 -o ProxyCommand="ssh -W %h:%p -i ~/.ssh/otusdevops otusdevops@35.210.212.166"

where 35.210.212.166 is extarnal IP of bastion and
10.132.0.3 is IP of someinternalhost.

In more general case to connect to any internal host through bastion
you can create file "~/.ssh/config" with the following content:

Host infrabastion
  Hostname 35.210.212.166
  User otusdevops
  IdentityFile  ~/.ssh/otusdevops
Host 10.132.0.*
  IdentityFile  ~/.ssh/otusdevops
  User otusdevops
  ProxyCommand ssh -W %h:%p  otusdevops@infrabastion

Then you can connect to any internal host from sub net 10.132.0.*
using command like:

ssh 10.132.0.3

************
