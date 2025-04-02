#

## Overview

The Unraid XML Template is used by Unraid to install both Docker Containers and Plugins. In both cases, it describes the program and points Unraid to the correct installation repository.

Squid, on the official Unraid forum, has a good [forum post](https://forums.unraid.net/topic/38619-docker-template-xml-schema/) going over the template. It was specifically made for Docker containers, but much of it is applicable to plugins as well.

## Plugin XML Template

### Examples

- [ich777/intel-gpu-top](https://github.com/ich777/docker-templates/blob/master/ich777/intel-gpu-top.xml)
- [Commifreak/unraid-appdata.backup](https://github.com/Commifreak/unraid-appdata.backup/blob/master/appdata.backup.plg)
- [linuxserver/Unraid-Nvidia](https://github.com/linuxserver/linuxserver-Plugin-Repository/blob/master/Unraid-Nvidia.xml)

## DockerMan XML Template

### Examples

- [linuxserver/plex](https://github.com/linuxserver/templates/blob/main/unraid/plex.xml)
- [selfhosters/cadvisor](https://github.com/selfhosters/unRAID-CA-templates/blob/master/templates/cadvisor.xml)