# Docker Manage Hosts

This role is a collections of plays that call the Docker api.

## Requirements

The Control Node must have Docker installed.

## Role Variables

The [defaults/main.yml](defaults/main.yml) file contains the following variables:

| Variable | Description | Example |
|----------|----------|---------|
| dkr_volumes | List of Docker volumes to map | (see file) |

Below is a table of common variables:

| Variable | Description | Example |
|----------|----------|---------|
| taskname | Select Docker task to perform | start_host </br> delete_host </br> build_dockerfile </br> delete_image </br>  create_image_from_container |

The following sections describe the variables for each task.

#### build_dockerfile

| Variable | Description | Example |
|----------|----------|---------|
| image_name | The name of the Docker image to build | c7-systemd |
| image_tag | Docker image tag | 1 |
| dockerfile | Name of the Dockerfile to use | dockerfile.c7-systemd |

#### create_image_from_container

| Variable | Description | Example |
|----------|----------|---------|
| dkr_container | Name of the Docker container | happy_einstein |
| dkr_image | Name of the Docker image | my_docker_image |
| dkr_command | Docker image entrypoint command | `/entrypoint.sh` |
| dkr_tag | Docker image tag | 1 |

#### delete_host

| Variable | Description | Example |
|----------|----------|---------|
| host_list | List of Docker containers to delete | - container1 </br> - container2|
| dkr_image | Name of container's base image | centos:7 |

#### start_host

| Variable | Description | Example |
|----------|----------|---------|
| host_group | Ansible group name to add the containers to | managed |
| host_list | Dictionary of container data | see [defaults/docker_hosts.yml](defaults/docker_hosts.yml) |
| dkr_command | Docker image entrypoint command | `sleep infinity` |
| dkr_privilege | Container privilege state | yes or no |
| dkr_volumes | Docker volumes to map to host | see [defaults/docker_hosts.yml](defaults/docker_hosts.yml) |

## Dependencies

None.

## Testing the role

The `main.yml` file tests the plays and is called as follows:

```yaml
---
- name: Converge
  hosts: all
  pre_tasks:
    - name: Install pre-requisites
      include_tasks: "pre_requisites.yml"
  roles:
    - { role: docker_manage_hosts, taskname: "start_host" }
    - { role: docker_manage_hosts, taskname: "delete_host" }
    - { role: docker_manage_hosts, taskname: "build_dockerfile", image_name: "c7-systemd", image_tag: "1", dockerfile: "dockerfile.c7-systemd" }
    - { role: docker_manage_hosts, taskname: "delete_image", dkr_image: "c7-systemd:1" }
...
```
