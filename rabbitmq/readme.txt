1.��ȡ����docker pull rabbitmq:3.6.16-management;
2.��������docker network create rabbitmq-net; 
3.���������������˿ڷֱ�Ϊ 5672/15672--5674/15674
docker run -d \
-p 5672:5672 \					#5673:5672    5674:5672
-p 15672:15672 \				#15673:15672    15674:15672
-e RABBITMQ_NODENAME=rabbitmq1 \	#rabbitmq2  rabbitmq3
-e RABBITMQ_ERLANG_COOKIE='SELLERPROERP' \
-h rabbitmq1 \      #rabbitmq2  rabbitmq3
--name=rabbitmq1 \		#rabbitmq2  rabbitmq3
--net=rabbitmq-net \
rabbitmq:3.6.16-management

4.�ֱ����ڶ���������������ִ��
root@rabbitmq2:/# rabbitmqctl -n rabbitmq2@rabbitmq2 -q stop_app
root@rabbitmq2:/# rabbitmqctl -n rabbitmq2@rabbitmq2 -q reset   
root@rabbitmq2:/# rabbitmqctl -n rabbitmq2@rabbitmq2 -q join_cluster rabbitmq1@rabbitmq1
root@rabbitmq2:/# rabbitmqctl -n rabbitmq2@rabbitmq2 -q start_app

root@rabbitmq3:/# rabbitmqctl -n rabbitmq3@rabbitmq3 -q stop_app
root@rabbitmq3:/# rabbitmqctl -n rabbitmq3@rabbitmq3 -q reset   
root@rabbitmq3:/# rabbitmqctl -n rabbitmq3@rabbitmq3 -q join_cluster rabbitmq1@rabbitmq1 --ram    #����������ڵ�����Ϊ�ڴ�ڵ�
root@rabbitmq3:/# rabbitmqctl -n rabbitmq3@rabbitmq3 -q start_app

5.��ɼ�Ⱥ���鿴״̬��
http://server02:15672/      �û���guest������guest