# jira

# installing docker

exec 3>&1 && exec 3> /dev/null

( grep -i 'centos' /etc/redhat-release ) 1>&3 || { echo "Please use CentOS" ; exit 6 ; }

( rpm -qa | grep -i epel-release )  1>&3 || { yum install epel-release -y ; sleep 3 ; yum install ansible -y ; }

sleep 3

ansible-pull -i inventory -U https://github.com/praveensams/jira  wrap.yml -e 'host_name=localhost playbook=docker'

exec 1>&3-
