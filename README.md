Задание 1
--Install and configure Zabbix for your platform--
1. Install Zabbix repository
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
dpkg -i zabbix-release_6.0-4+debian11_all.deb
apt update
2. Install Zabbix server, frontend, agent
apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts
3. Create initial database
Run the following on your database host.
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
On Zabbix server host import initial schema and data. You will be prompted to enter your newly created password.
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
4. Configure the database for Zabbix server
Edit file /etc/zabbix/zabbix_server.conf
sed -i 's/# DBPassword=/DBPassword=123/g' /etc/zabbix/zabbix_server.conf
5. Start Zabbix server and agent processes
Start Zabbix server and agent processes and make it start at system boot.
systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2

![alt text](https://github.com/rus42/zabbix/blob/main/Task_1.png)

Задание 2

Debian
1. Install Zabbix agent on Zabbix server
apt install zabbix-agent
2. Start Zabbix agent process
Start Zabbix agent process and make it start at system boot.
systemctl restart zabbix-agent
systemctl enable zabbix-agent

Ubuntu
1. Install Zabbix repository
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu22.04_all.deb
dpkg -i zabbix-release_6.0-4+ubuntu22.04_all.deb
apt update
2. Install Zabbix agent
apt install zabbix-agent
sed -i 's/Server=127.0.0.1/Server=192.168.1.119/g' /etc/zabbix/zabbix_agentd.conf
sed -i 's/ServerActive=127.0.0.1/ServerActive=192.168.1.119/g' /etc/zabbix/zabbix_agentd.conf
3. Start Zabbix agent process
Start Zabbix agent process and make it start at system boot.
systemctl restart zabbix-agent
systemctl enable zabbix-agent

cat /var/log/zabbix/zabbix_agentd.log

![alt text](https://github.com/rus42/zabbix/blob/main/Task_2.1.png)
![alt text](https://github.com/rus42/zabbix/blob/main/Task_2.2.png)
![alt text](https://github.com/rus42/zabbix/blob/main/Task_2.3.1.png)
![alt text](https://github.com/rus42/zabbix/blob/main/Task_2.3.2.png)

Задание 3

![alt text](https://github.com/rus42/zabbix/blob/main/Task_3.png)


