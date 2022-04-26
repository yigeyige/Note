#**rabbitMQ**  
**author: YIGe**  
**date: 2021/3/10 16:01** 

1. rabbitMQ搭建  
    + 创建用户  
        ```shell script
        cd rabbitmq/sbin
        sudo ./rabbitmqctl add_user admin admin
        sudo ./rabbitmqctl set_user_tags admin administrator
        sudo ./rabbitmqctl set_permissions admin ".*"  ".*"  ".*"
        ```


2. rabbitMQ状态  
    + 查询队列状态  
        ```shell script
        curl -u admin:admin http://127.0.0.1:15672/api/queues/%2F/testQueue
        ```
    - 结果值分析  
        引用链接：[rabbit分析](https://www.cnblogs.com/biehongli/p/11789098.html)
        ```json
        {
        	"consumer_details": [],
        	"arguments": {
        		
        	},
        	"auto_delete": false,
        	"backing_queue_status": {
        		"avg_ack_egress_rate": 0.0,
        		"avg_ack_ingress_rate": 0.0,
        		"avg_egress_rate": 0.0,
        		"avg_ingress_rate": 0.002972661140015964,
        		"delta": ["delta",
        		"undefined",
        		0,
        		0,
        		"undefined"],
        		"len": 12601,
        		"mode": "default",
        		"next_seq_id": 18008,
        		"q1": 0,
        		"q2": 0,
        		"q3": 0,
        		"q4": 12601,
        		"target_ram_count": "infinity"
        	},
        	"consumer_utilisation": null,
        	"consumers": 0,
        	"deliveries": [],
        	"durable": true,
        	"effective_policy_definition": [],
        	"exclusive": false,
        	"exclusive_consumer_tag": null,
        	"garbage_collection": {
        		"fullsweep_after": 65535,
        		"max_heap_size": 0,
        		"min_bin_vheap_size": 46422,
        		"min_heap_size": 233,
        		"minor_gcs": 981
        	},
        	"head_message_timestamp": null,
        	"idle_since": "2022-03-26 7:30:01",
        	"incoming": [],
        	"memory": 18710048,
        	"message_bytes": 163813,
        	"message_bytes_paged_out": 0,
        	"message_bytes_persistent": 163813,
        	"message_bytes_ram": 163813,
        	"message_bytes_ready": 163813,
        	"message_bytes_unacknowledged": 0,
        	"message_stats": {
        		"ack": 5407, 
        		"ack_details": {
        			"rate": 0.0
        		},
        		"deliver": 5481,
        		"deliver_details": {
        			"rate": 0.0
        		},
        		"deliver_get": 5481,
        		"deliver_get_details": {
        			"rate": 0.0
        		},
        		"deliver_no_ack": 0,
        		"deliver_no_ack_details": {
        			"rate": 0.0
        		},
        		"get": 0,
        		"get_details": {
        			"rate": 0.0
        		},
        		"get_no_ack": 0,
        		"get_no_ack_details": {
        			"rate": 0.0
        		},
        		"publish": 18008,
        		"publish_details": {
        			"rate": 0.0
        		},
        		"redeliver": 70,
        		"redeliver_details": {
        			"rate": 0.0
        		}
        	},
        	"messages": 12601,
        	"messages_details": {
        		"rate": 0.0
        	},
        	"messages_paged_out": 0,
        	"messages_persistent": 12601,
        	"messages_ram": 12601,
        	"messages_ready": 12601,
        	"messages_ready_details": {
        		"rate": 0.0
        	},
        	"messages_ready_ram": 12601,
        	"messages_unacknowledged": 0,
        	"messages_unacknowledged_details": {
        		"rate": 0.0
        	},
        	"messages_unacknowledged_ram": 0,
        	"name": "oaQueue",
        	"node": "rabbit@zdbzxtvpca06",
        	"operator_policy": null,
        	"policy": null,
        	"recoverable_slaves": null,
        	"reductions": 392090103,
        	"reductions_details": {
        		"rate": 0.0
        	},
        	"state": "running",
        	"vhost": "/"
        }
        ```
        message_stats.ack 代表消息正常消费并反馈结果给队列；  
        