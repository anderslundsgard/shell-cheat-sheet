# shell-cheat-sheet
Various random Linux shell/bash commands

## Install nginx on Debian
```
sudo apt update;
sudo apt install nginx -y;
```

## Generate random password
```
pwgen -c -Bs 48 1
```

## Generate ssh key
```
ssh-keygen -b 2048 -t rsa
```

## Print tail for cloud-init log
```
sudo tail -f /var/log/cloud-init-output.log
```

## curl AWS meta-data endpoint
```
curl http://169.254.169.254/latest/meta-data/instance-id
```

## Pull image from ECR
```
sudo -s
docker image ls
aws sts get-caller-identity
aws ecr get-login-password --region eu-west-1 | docker login --username AWS --password-stdin 123456789098.dkr.ecr.eu-west-1.amazonaws.com
docker image pull 123456789098.dkr.ecr.eu-west-1.amazonaws.com/my-image:v21
docker image ls
```

## Install and connect to postgresql

### RDS notes 
- Same endpoint generated id per account per region
- Create snapshot -> Copy with encryption -> Restore with new name -> Remove old instance -> Rename new to old name
- Share between Accounts but in same region

```
sudo yum install -y postgresql

psql --host=main-postgres.abcdefghijkl.eu-west-1.rds.amazonaws.com --dbname=postgres --password --username=postgres

...pwd...

select * from user_schema.roles;

CREATE USER db_user;
GRANT rds_iam TO db_user;

CREATE TABLE distributors (did integer CHECK (did > 10), name varchar(40));
INSERT INTO distributors (did, name) VALUES (11, 'Bananbo Yxa');
SELECT * FROM distributors;
\l
\q
```
