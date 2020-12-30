# lightsail-home-assistant
Home Assistant installation on AWS Lightsail

## Create instance
Create AWS Lightsail instance via [AWS Lightsail CLI](https://docs.aws.amazon.com/cli/latest/reference/lightsail/index.html "AWS Lightsail CLI")
```
aws lightsail create-instances --instance-names "ha-vm" --availability-zone eu-west-2a --blueprint-id amazon_linux_2 --bundle-id micro_2_0 --user-data file://user-data.txt
```
You can find the script in `/var/lib/cloud/instance/user-data.txt` on the instance

## Configure instance
### Open ports
```
aws lightsail open-instance-public-ports --port-info fromPort=443,toPort=443,protocol=TCP --instance-name ha-vm
```
## Deploy IoT Republish rules via CloudFormation
```
aws cloudformation deploy --template-file iot-rules-cfn.yaml --stack-name iot-stack --capabilities CAPABILITY_IAM
```

## Monitoring IoT
https://docs.aws.amazon.com/iot/latest/developerguide/configure-logging.html