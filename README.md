# amazon-sns-resource-agent

Pacemaker Resource Agent for Amazon SNS

This resource agent script is intended for Linux operating systems and Pacemaker.

## Prerequisites

This script requires [AWS Command Line Interface](http://aws.amazon.com/cli/).

Some IAM policies requires. Here's an example setting:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Stmt1481000000000",
            "Effect": "Allow",
            "Action": [
                "sns:ListTopics"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Sid": "Stmt1481000000000",
            "Effect": "Allow",
            "Action": [
                "sns:Publish"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


## Getting Started

Download "AmazonSNS" or clone repository:

```sh
git clone https://github.com/yomon8/amazon-sns-resource-agent.git
cd amazon-sns-resource-agent
```

Install AmazonSNS resource agent:
```
mv AmazonSNS /usr/lib/ocf/resource.d/heartbeat/
chown root:root /usr/lib/ocf/resource.d/heartbeat/AmazonSNS 
chmod 0755 /usr/lib/ocf/resource.d/heartbeat/AmazonSNS
```

Install check

```
$ pcs resource list | grep AmazonSNS
ocf:heartbeat:AmazonSNS - Notifies recipients by Amazon SNS in the event of
```

After setting up pacemaker, configure resource agent by pcs command. Here's an example setting:

```
pcs resource create res-amazon-sns ocf:heartbeat:AmazonSNS \
   params \
      topic_arn=arn:aws:sns:ap-northeast-1:123456789012:topic_name \
      subject=ClusterName \
   op monitor timeout="10s" interval="10s"
```

# Parameters

Name	|Description
-------------------------- | -------------------------------------------------
topic_arn | Amazon SNS Topic Arn you want to publish to 
subject | Text head of the subject line 



