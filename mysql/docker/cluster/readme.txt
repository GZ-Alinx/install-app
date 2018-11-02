1.���ؾ���
   docker pull mysql:5.7
2.���������ļ�������Ŀ¼
   mkdir /usr/local/mysql/master/m1/conf -p��
   mkdir /usr/local/mysql/master/m1/conf/data -p��
   touch master.cnf��
3.�����������ļ���Ŀ¼����master
	docker run -p 3301:3306 --name mysql-m1 -v /usr/local/mysql/master/m1/conf:/etc/mysql/conf.d -v /usr/local/mysql57/master/m1/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=654321 -d mysql:5.7��

4.��������docker exec -it mysql-m1 mysql -p
5.�鿴master״̬ show master status \G��
6.���������û���CREATE USER 'repl'@'%' IDENTIFIED BY 'repl';��GRANT REPLICATION SLAVE ON *.* TO 'repl'@'%';

7.ͬ������slaves�ڵ�
	
	docker run --name mysql-slave \
-v /home/mysql/etc/slave:/etc/mysql/conf.d \
-v /home/mysql/data/slave:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=root \
--link mysql-master:master \
-d mysql:5.7

8.����ӽڵ��������������ӣ�
stop slave;

CHANGE MASTER TO \
MASTER_HOST='master',\
MASTER_PORT=3306,\
MASTER_USER='repl',\
MASTER_PASSWORD='repl',\
MASTER_LOG_FILE='binlog.000008',\
MASTER_LOG_POS=595;

start slave;
9.��ɣ�
10.�ظ��������4��4�ӣ�
