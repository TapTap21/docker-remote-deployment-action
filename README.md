# Docker Deployment Action
A [GitHub Action](https://github.com/marketplace/actions/docker-compose-remote-deployment) for docker-compose deployments on a remote host using SSH.

The Action is adapted from work by [wshihadeh](https://github.com/marketplace/actions/docker-deployment)


## Example

Below is an example of how the action can be used

```yaml
- name: Start Deployment
  uses: TapTap21/docker-remote-deployment-action@v1.0
  with:
    remote_docker_host: ec2-user@ec2-34-246-134-80.eu-west-1.compute.amazonaws.com
    ssh_private_key: ${{ secrets.DOCKER_SSH_PRIVATE_KEY }}
    ssh_public_key: ${{ secrets.DOCKER_SSH_PUBLIC_KEY }}
    stack_file_name: docker-compose.yml
    docker_login_password: ${{ secrets.DOCKER_REPO_PASSWORD }}
    docker_login_user: ${{ secrets.DOCKER_REPO_USERNAME }}
    docker_login_registry : ${{ steps.login-ecr.outputs.registry }}
    args: -p myapp up -d
```

Use the latest tag to run the latest build or a specific version tag. The action pulls a docker image instead of building one to improve performance.
## Input

Below is a breakdown of the expected action inputs.

### `args`

Docker-compose runtime arguments and options. Below is a common usage example:

- `-p app_stack_name -d up`

### `remote_docker_host`

Specify Remote Docker host. The input value must be in the following format (user@host)

### `ssh_public_key`

Remote Docker SSH public key.

### `ssh_private_key`

SSH private key used to connect to the docker host.

SSH key must be in PEM format (begins with -----BEGIN RSA PRIVATE KEY-----)

### `ssh_port`

The SSH port to be used. Default is 22.

### `stack_file_name`

Docker stack file used. Default is docker-compose.yml

### `docker_login_user`

The username for the container repository user. (DockerHub, ECR, etc.)

### `docker_login_password`

The password for the container repository user.

### `docker_login_registry`

The docker container registry to authenticate against

## License

This project is licensed under the MIT license. See the [LICENSE](LICENSE) file for details.
