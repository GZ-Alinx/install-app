1.��װ������docker
2.��ȡredis(4.0.9)��ruby����
	
	docker pull redis
	docker pull ruby	

3.����6���ڵ�������ļ� portΪ��7000/17000--7005/17005��
	�� redis.conf��

4.����6���ڵ�����ݴ洢Ŀ¼ data

5.����redis����  
	docker network create redis-net

6.����6��redis����
	ʹ��cluster.sh����6��������ע���޸����й����ļ���Ŀ¼

7.ʹ��rubyʵ�ּ�Ⱥ
	trib.sh

8.���