[![build-test](https://github.com/darkwizard242/ansible-role-kubelet/workflows/build-and-test/badge.svg?branch=master)](https://github.com/darkwizard242/ansible-role-kubelet/actions?query=workflow%3Abuild-and-test) [![release](https://github.com/darkwizard242/ansible-role-kubelet/workflows/release/badge.svg)](https://github.com/darkwizard242/ansible-role-kubelet/actions?query=workflow%3Arelease) ![Ansible Role](https://img.shields.io/ansible/role/57090?color=dark%20green%20) ![Ansible Role](https://img.shields.io/ansible/role/d/57090?label=role%20downloads) ![Ansible Quality Score](https://img.shields.io/ansible/quality/57090?label=ansible%20quality%20score) [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=ansible-role-kubelet&metric=alert_status)](https://sonarcloud.io/dashboard?id=ansible-role-kubelet) [![Maintainability Rating](https://sonarcloud.io/api/project_badges/measure?project=ansible-role-kubelet&metric=sqale_rating)](https://sonarcloud.io/dashboard?id=ansible-role-kubelet) [![Reliability Rating](https://sonarcloud.io/api/project_badges/measure?project=ansible-role-kubelet&metric=reliability_rating)](https://sonarcloud.io/dashboard?id=ansible-role-kubelet) [![Security Rating](https://sonarcloud.io/api/project_badges/measure?project=ansible-role-kubelet&metric=security_rating)](https://sonarcloud.io/dashboard?id=ansible-role-kubelet) ![GitHub tag (latest SemVer)](https://img.shields.io/github/tag/darkwizard242/ansible-role-kubelet?label=release) ![GitHub repo size](https://img.shields.io/github/repo-size/darkwizard242/ansible-role-kubelet?color=orange&style=flat-square)

# Ansible Role: kubelet

Role to install (_by default_) [kubelet](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/) on **Debian/Ubuntu** and **EL** systems.

## Requirements

None.

## Role Variables

Available variables are listed below (located in `defaults/main.yml`):

### Variables list:

```yaml
kubelet_app: kubelet
kubelet_version: 1.26.6
kubelet_os: linux
kubelet_arch: amd64
kubelet_dl_url: https://dl.k8s.io/release/v{{ kubelet_version }}/bin/{{ kubelet_os }}/{{ kubelet_arch }}/{{ kubelet_app }}
kubelet_bin_path: /usr/local/bin
kubelet_file_mode: '0755'
kubelet_systemd_service_setup: true
kubelet_systemd_template_out_dir: /etc/systemd/system
kubelet_systemd_template_in_file: kubelet.service.j2
kubelet_systemd_template_out_file: kubelet.service
kubelet_systemd_dropin_dir: "{{ kubelet_systemd_template_out_dir }}/{{ kubelet_app }}.service.d"
kubelet_systemd_dropin_source_file: 10-kubeadm.conf.j2
kubelet_systemd_dropin_dest_file: 10-kubeadm.conf
kubelet_systemd_service_enable_state: yes
kubelet_systemd_service_state: started
```

### Variables table:

Variable                             | Description
------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------
kubelet_app                          | Defines the app to install i.e. **kubelet**
kubelet_version                      | Defined to dynamically fetch the desired version to install. Defaults to: **1.26.6**
kubelet_os                           | Defines OS type. Defaults to: **linux**
kubelet_arch                         | Defines os architecture. Used for obtaining the correct type of binaries based on OS System Architecture. Defaults to: **amd64**
kubelet_dl_url                       | Defines URL to download the kubelet binary from.
kubelet_bin_path                     | Defined to dynamically set the appropriate path to store kubelet binary into. Defaults to (as generally available on any user's PATH): **/usr/local/bin**
kubelet_file_mode                    | Mode for the binary file of kubelet.
kubelet_systemd_service_setup        | Boolean for whether systemd service setup (systemd service generation, systemd boot start and state change) for kubelet needs to be performed.
kubelet_systemd_template_out_dir     | Destination directory to store the generated Jinja template for kubelet's systemd service.
kubelet_systemd_template_in_file     | Template (Jinja) file to use as source for kubelet's systemd service.
kubelet_systemd_template_out_file    | Destination filename for kubelet's systemd service.
kubelet_systemd_dropin_dir           | Directory to store the systemd drop-in for kubelet.
kubelet_systemd_dropin_source_file   | Source template for kubelet's systemd-dropin.
kubelet_systemd_dropin_dest_file     | Destination filename for kubelet's systemd-dropin.
kubelet_systemd_service_enable_state | Defined to enable kubelet systemd service at boot.
kubelet_systemd_service_state        | Defined to set the state of the kubelet systemd service

## Dependencies

None

## Example Playbook

For default behaviour of role (i.e. installation of **kubelet**) in ansible playbooks.

```yaml
- hosts: servers
  roles:
    - darkwizard242.kubelet
```

For customizing behavior of role (i.e. specifying the desired **kubelet** version) in ansible playbooks.

```yaml
- hosts: servers
  roles:
    - darkwizard242.kubelet
  vars:
    kubelet_version: 1.22.0
```

For customizing behavior of role (i.e. placing binary of **kubelet** package in different location) in ansible playbooks.

```yaml
- hosts: servers
  roles:
    - darkwizard242.kubelet
  vars:
    kubelet_bin_path: /bin/
```

## License

[MIT](https://github.com/darkwizard242/ansible-role-kubelet/blob/master/LICENSE)

## Author Information

This role was created by [Ali Muhammad](https://www.alimuhammad.dev/)
