---
title: "Aws"
date: 2019-05-31T11:08:33+02:00
draft: true
---

# Use the aws commandline tool

To get a list of your ec2 instances with their decriptions:

```
aws ec2 describe-instances
```

to get for example the public dns for your instances:

```
aws ec2 describe-instances | jq .Reservations[0].Instances[0].PublicDnsName
```


