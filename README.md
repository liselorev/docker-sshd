# SSHD

[![Docker Repository on docker.com](https://hub.docker.com/r/liselorev/docker-sshd/status "Docker Repository on docker.com")](https://hub.docker.com/r/liselorev/docker-sshd)

Forked from macropin/docker-ssh

Minimal Alpine Linux Docker container with `sshd` exposed and `rsync` installed.

Mount your .ssh credentials (RSA public keys) at `/root/.ssh/` in order to
access the container via root ssh or mount each user's key in
`/etc/authorized_keys/<username>` and set `SSH_SERS` config to create user accounts (see below).

Optionally mount a custom sshd config at `/etc/ssh/`.
Optionally mount a (target) user home directory (at /homes/username).

## Environment Options

- `SSH_USERS` list of user accounts and uids/gids to create. eg `SSH_USERS=www:48:48,admin:1000:1000`
- `MOTD` change the login message

## Usage Example

```
docker run -d -p 2222:22 -v /secrets/id_rsa.pub:/root/.ssh/authorized_keys -v /mnt/data/:/data/ liselorev/docker-sshd
```

or

```
docker run -d -p 2222:22 -v $(pwd)/id_rsa.pub:/etc/authorized_keys/www -e SSH_USERS="www:48:48" liselorev/docker-sshd
```

or

```
docker run -d -p 2222:22 -v $(pwd)/id_rsa.pub:/etc/authorized_keys/username -e SSH_USERS="username:1113:1000" liselorev/docker-sshd
```
