# ansible-local-aws


## Installation
Install [Amazon AWS Collection](https://docs.ansible.com/ansible/latest/collections/amazon/aws/index.html) for Ansible:
```
ansible-galaxy collection install community.aws amazon.aws
```

Create a temporary directory for Docker volume mapping:

```
mkdir -p /tmp/localstack/data
```

Create a docker network:

```
docker network create abrar_localcloud_0  
```

Bring up the container:

```
docker-compose up -d
```

Run the container:

```
docker-compose start
```

Check if the container is running:

```
docker ps
```

Search for the container and get the ID. Then execute the container shell:

```
docker exec -it YOUR_CONTAINER_ID sh
```

Create a user:

```
awslocal iam create-user --user-name admin
```


Check if the user is created successfully:

```
awslocal iam list-users
```
You will find user `admin` in the list

Create a access key:

```
awslocal iam create-access-key --user-name admin
```

Get the `AccessKeyId` and `SecretAccessKey` values from the above command's output. We will pass them to the Ansible Playbook as extra variables

Run the Ansible playbook:

```
ansible-playbook aws_create_user.yml --extra-vars "ACCESS_KEY_ID=YOUR_AWS_ACCESS_KEY_ID SECRET_ACCESS_KEY=YOUR_SECRET_ACCESS_KEY"
```