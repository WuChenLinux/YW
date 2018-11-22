---
layout: post
title: 'alertmanager ��Ĭ����'
date: 2018-11-22
author: ����
color: rgb(255,210,32)
cover: 'https://open.saintic.com/api/bingPic/'
tags: Prometheus
---
# alertmanager ��Ĭ����

> �����õ��������Ĭ���򣬼�¼�� 
>
> ʹ�õ��ǹٷ�docker����https://hub.docker.com/r/prom/alertmanager/
>
> �ٷ�github��ַ:  https://github.com/prometheus/alertmanager   

docker hub �ϵļܹ�ͼ����������

![1542879471951](https://wuchen-1252812685.cos.ap-shanghai.myqcloud.com/img/11-22-alertmanager-amtool/1542879471951.png)





��������֮�󣬽��뵽������

```shell
#����Ҫ�Ķ�����������������������������
#֮ǰֻ�Ǽ򵥵� amtool -h�ˣ��������Լ�
amtool --help-long
```

�����ļ���ַ

```shell
cat /etc/amtool/config.yml   

#alertmanager��ַ,���ﶨ����֮���������п��Բ��� --alertmanager.url="http://127.0.0.1:9093"
alertmanager.url: "http://localhost:9093"

#�ύ��
author: wuchen

#�Ƿ���Ҫ��ע�����ύ��Ĭ��true������Ҫ��ע
comment_required: false

#����Ĭ�������ʽ
output: extended

#Ĭ�Ͻ�����������ʱ�������
receiver: webhook
```




```shell
#�鿴��ǰ�Ѵ����ı���
amtool alert --alertmanager.url="http://127.0.0.1:9093"

#�鿴���г�Ĭ
amtool silence query --alertmanager.url="http://127.0.0.1:9093"

#�鿴ƥ��ĳ�Ĭ
amtool silence query alertname=PodMemory  --alertmanager.url="http://127.0.0.1:9093"


#��Ĭ��ӣ����comment_required����Ϊtrue����дcomment�Ļ����ύ����
#alertname����Prometheus�������õ�alert
#--start ��Чʱ��
#--end   ����ʱ��
amtool silence add alertname="PodMemory" container_name="elasticsearch" --start="2019-01-02T15:04:05+08:00" --end="2019-01-02T15:05:05+08:00" --comment="test"  -a "wuchen" --alertmanager.url="http://127.0.0.1:9093"

#docker�ٷ�����Ĭ������Դ������/alertmanager������Ҫ���������̣���Ȼ��������һ�ж�����

#��Ϊ�鿴��Ĭ�б��ʱ����Чʱ������Ĳ����������Կ���
amtool silence query -o json --alertmanager.url="http://127.0.0.1:9093"
#�����Ե���json����
amtool silence query -o json PodMemory > 1.json --alertmanager.url="http://127.0.0.1:9093"

#��Ĭ���
amtool silence expire 8188b168-1332-4398-83a5-a9df4263c60d --alertmanager.url="http://127.0.0.1:9093"

#������г�Ĭ
amtool silence expire $(amtool silence query -q --alertmanager.url="http://127.0.0.1:9093") --alertmanager.url="http://127.0.0.1:9093"


```

���������ǰ�����Դ���õ���/alertmanager�����ǹ���һ�������̵����Ŀ¼�ͺ��ˣ���Ȼ����������һ�в�����û�ˡ�

�ţ��ͼ�¼�¡�