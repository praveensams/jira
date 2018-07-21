# jira installation 

# installing docker (centos)


[ $(id -u) -eq 0 ] || { echo 'try with root'; exit 6; }

exec 3>&1 && exec 3> /dev/null

( netstat -ntpl | grep 8080 ) 1>&3 && { echo "Please free 8080 port " ; exit 6 ; }

( grep -i 'centos' /etc/redhat-release ) 1>&3 || { echo "Please use CentOS" ; exit 6; }

( ps aux | grep -i docker ) && { docker -qa | xargs docker rm ; }

( rpm -qa | grep -i epel-release )  1>&3 || { yum install epel-release -y ; sleep 3 ; yum install ansible -y ; }

sleep 3

ansible-pull -i inventory -U https://github.com/praveensams/jira  wrap.yml -e 'host_name=localhost playbook=docker'

sleep 3

( netstat -ntpl | grep 8080 ) || { echo "Port 8080 is not running , check for existing service binding to port 8080" ; exit 6; } 



clear

echo "
#################################################################
#                                                               #
#                                                               #
#       Jira service installed please check                     #
#                                                               #
#             http://ipaddress:8080                             #
#                                                               #
#                                                               #
#################################################################
"
exec 1>&3-
