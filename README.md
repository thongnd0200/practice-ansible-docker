### 1. 環境の準備

```
# get source ansible playbook
git clone https://github.com/thongnd0200/practice-ansible-docker.git

# get source application
cd practice-ansible-docker
git clone https://github.com/thongnd0200/yii2-project.git

# create log dir
cd yii2-project
mkdir log

# start VMs
vagrant up ci consumer

# install for ci and consumer
vagrant ssh ci
cd practice-ansible-docker
ansible-playbook -i hosts.local provision.yml --become

# install mysql by docker-compser
ansible-playbook -i hosts.local install_mysql.yml --become

# install nginx-php-fpm by docker-compser
ansible-playbook -i hosts.local deploy_app.yml --become
exit

# php init
vagrant ssh consumer
sudo docker exec -it php-fpm bash
cd /code/ && php init


# add local hosts file
192.168.33.91   frontend.yii2
192.168.33.91   backend.yii2

#Confirm start web: Browser
http://frontend.yii2

# CASE vendor error
vagrant ssh consumer
sudo docker exec -it php-fpm bash
cd /code/
rm -r vendor/
composer install
```
