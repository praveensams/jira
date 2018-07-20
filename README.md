# jira installation 

# installing docker

[ $(id -u) -eq 0 ] || { echo 'try with root'; kill $$; }

exec 3>&1 && exec 3> /dev/null

( netstat -ntpl | grep 8080 ) && { echo "Please free 8080 port " ; kill $$ ; }

( grep -i 'centos' /etc/redhat-release ) 1>&3 || { echo "Please use CentOS" ; kill $$ ; }

( rpm -qa | grep -i epel-release )  1>&3 || { yum install epel-release -y ; sleep 3 ; yum install ansible -y ; }

sleep 3

ansible-pull -i inventory -U https://github.com/praveensams/jira  wrap.yml -e 'host_name=localhost playbook=docker'

sleep 3

( netstat -ntpl | grep 8080 ) || { echo "Port 8080 is not running , check for existing service binding to port 8080" ; kill $$ ; } 

exec 1>&3-


tput clear


#################################################################
#                                                               #
#                                                               #
#       Jira service installed please check                     #
#                                                               #
#             http://ipaddress:8080                             #
#                                                               #
#                                                               #
#################################################################
