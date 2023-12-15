# ubuntu-sshd-cron

Integrate SSH and CRON services and start automatically. Built on [Official Ubuntu](https://registry.hub.docker.com/_/ubuntu/) image.

![](https://img.shields.io/badge/multiarch-amd64*i386*arm64*armv7*armv6*ppc64le-blue?labelColor=blue&color=deep%2520green)
![](https://img.shields.io/github/actions/workflow/status/binge8/ubuntu/ubuntu.yml?labelColor=blue)

![](https://img.shields.io/docker/image-size/bin20088/ubuntu?labelColor=blue&color=deep%20green)
![](https://img.shields.io/docker/pulls/bin20088/ubuntu?labelColor=blue&color=deep%20green)
![](https://img.shields.io/docker/stars/bin20088/ubuntu?labelColor=blue&color=deep%20green)

## Image tags

- ubuntu:16.04
- ubuntu:18.04
- ubuntu:20.04
- ubuntu:22.04

Config:

  - `PermitRootLogin yes`
  - `UsePAM no`
  - exposed port 22
  - root password: `root`

## Run example

```bash
$ sudo docker run -d -P --name test_sshd rastasheep/ubuntu-sshd:14.04
$ sudo docker port test_sshd 22
  0.0.0.0:49154

$ ssh root@localhost -p 49154
# The password is `root`
root@test_sshd $
```

## Security

If you are making the container accessible from the internet you'll probably want to secure it bit.
You can do one of the following two things after launching the container:

- Change the root password: `docker exec -ti test_sshd passwd`
- Don't allow passwords at all, use keys instead:

```bash
$ docker exec test_sshd passwd -d root
$ docker cp file_on_host_with_allowed_public_keys test_sshd:/root/.ssh/authorized_keys
$ docker exec test_sshd chown root:root /root/.ssh/authorized_keys
```
