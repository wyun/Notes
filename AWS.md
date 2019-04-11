# AWS

## Setup

Under my account, click on 'Security Credentials'. for now, use standard security credentials, not the IAM one.  The access key is required for CLI.
- Access Keys:
```
Access Key ID:
    AKIAITZWIKMPD7LT2IUQ
Secret Access Key:
    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
```

- In configuration's output format, put `json`; 
- Check ec2: `aws ec2 describe-instances`. output should be a json object.

## IAM

New user is created. deleted root access. 

After setting up password, use IAM users sign in link:

https://834747298770.signin.aws.amazon.com/console
user: wjay
PW: Hu7ubcpR3

Elastic IP: 3.94.147.109

ssh -i <pem-file> ec2-user@elastic_ip

ssh -i /c/Users/wangy9/Downloads/pizza-keys.pem ec2-user@3.94.147.109

Use scp to copy node app to ec2 instance
```
scp -r -i <perm_file> <local_code> ec2-user@<ec2-ip>:/home/ec2-user/pizza-luvrs
```

#!/bin/bash
echo "starting pizza-luvrs"
nvm use v6.3.0
cd "/home/ec2-user/pizza-luvrs"
npm start