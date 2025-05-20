### Setting up awscli

1. Run aws configure cmd 
aws configure 

Test to make sure awscli is properly configured(command should not have an error output)
aws s3 ls

###################
###### logging into remote ec2 instance

1. move key into home directory
 mv mohammed-key.pem ~
 # verify that key has moved to home directory
 cd ~
 ll

2. change key permission to read only ## (only have do this once with new key)
chmod 400 mohammed-key.pem (*note not part of cmd- change to current/correct key name where necessary)

3. verify that key has been moved and has read only permissions
cd ~
ll

4. Remote login to ec2-instance using ssh command (Remember! Public ip will change everytime you restart the instance)
ssh -i (~/keyname) (username)@(publicipofinstance)
ssh -i ~/mohammed-key.pem ec2-user@3.145.172.180

### Alias for instance table
li

### To start instance
aws ec2 start-instances --instance-id i-058e5992bcad2faa0

### To stop instance 
aws ec2 stop-instances --instance-id  i-058e5992bcad2faa0

### To describe instance (This is a script.Run this from the local machine before logging into remote)
aws ec2 describe-instances --query "Reservations[*].Instances[*].{PublicIP:PublicIpAddress,Name:Tags[?Key=='Name']|[0].Value,Status:State.Name,ElasticIPAddress:ElasticIpAddress,InstanceID:InstanceId,InstanceType:InstanceType,SubnetID:SubnetId,VPCID:VpcId}" --output table | grep -v terminated

### Creating script for aws describe command
1. create a file for script 
vi ds.sh 

## To be a root user
sudo -i

## To list block devices
lsblk

## update ec2 instance
sudo dnf update -y (-y means not to ask Yes )

## install lvm2
sudo dnf install lvm2 -y

## partition disk and change type for lvm
fdisk /dev/xvdb

## fdisk -l 
/dev/mapper/vol--g1-lv--1

vol-g1/lv-1
UUID=cebe80bc-7aa8-4d1f-b38e-1375501d1365

To create a lv with added Gig
lvcreate -L+ (volume size)G -n lv-2 vol-g1 

/dev/mapper/vol--g1-lv--2
d614e8b0-3c2f-4add-af50-718815a67e9e

### setup Git repo

