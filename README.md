# Ansible Environment in Docker
Originally created by **Omar McIver** on 18th September 2021

- [LinkedIn](https://www.linkedin.com/in/omarmciver/)
- [YouTube](https://www.youtube.com/c/OmarMcIver/)
- [Blog](https://www.omarmciver.com/)

If you want to have playbooks pre-loaded, ensure you copy files in to the /home/ folder before building the docker image.

## Build the docker image
```
docker build . -t ansible
```

## Run the docker image as a container
```
docker run --name ansible_container -it --rm -e SUB=SubscriptionName -e AKV=KeyVaultName -e PSK=SecretName_PrivateSSHKey -e PSP=SecretName_PrivateSSHKeyPassphrase -e PUB=SecretName_PublicSSHKey ansible
```
- `--rm` will delete the container as soon as you exit it. Omit this if you want to reuse the same container.

- In this example the running container is named `ansible_container`. You can set this to any name you like, but it must be used in later commands to retrieve files from the container.

- When the docker container launches you will be asked to authenticate using an Azure device code (it uses `az login` to connect to the KeyVault)

## Transfer files to / from the running docker container
To get files to/from a docker container... https://docs.docker.com/engine/reference/commandline/cp/
```
docker cp ansible_container:/root/somefolder E:/temp/
```